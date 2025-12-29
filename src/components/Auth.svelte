<script>
  import { onMount } from 'svelte';
  
  let isAuthenticated = false;
  let isLoading = false;
  let authError = null;
  let userInfo = null;
  
  // Check if super app's my object is available
  const checkSuperApp = () => {
    if (typeof window !== 'undefined' && window.my) {
      return true;
    }
    return false;
  };
  
  // Function to get auth code from super app
  const getAuthCode = async () => {
    if (!checkSuperApp()) {
      authError = 'Super app not detected. Please open this app in the super app environment.';
      return;
    }
    
    isLoading = true;
    authError = null;
    
    try {
      // Get auth code from super app
      window.my.getAuthCode({
        scopes: ['auth_base', 'USER_ID'],
        success: async (res) => {
          try {
            // Send auth code to MiniApps auth endpoint
            const response = await fetch('https://its.mouamle.space/api/auth-with-superQi', {
              method: 'POST',
              headers: {
                'Content-Type': 'application/json',
              },
              body: JSON.stringify({
                token: res.authCode
              })
            });
            
            if (response.ok) {
              const data = await response.json();
              userInfo = data.user;
              isAuthenticated = true;
              
              // Store auth token if provided
              if (data.token) {
                localStorage.setItem('authToken', data.token);
              }
              
              // Emit auth success event
              document.dispatchEvent(new CustomEvent('authSuccess', { detail: data }));
            } else {
              authError = 'Authentication failed on server';
            }
          } catch (error) {
            authError = 'Network error during authentication';
            console.error('Auth error:', error);
          } finally {
            isLoading = false;
          }
        },
        fail: (err) => {
          authError = `Authorization failed: ${err.authErrorScopes}`;
          isLoading = false;
          console.error('Authorization failed:', err);
        }
      });
    } catch (error) {
      authError = 'Unexpected error during authentication';
      isLoading = false;
      console.error('Unexpected error:', error);
    }
  };
  
  // Function to logout
  const logout = () => {
    isAuthenticated = false;
    userInfo = null;
    localStorage.removeItem('authToken');
    document.dispatchEvent(new CustomEvent('authLogout'));
  };
  
  // Check existing auth on mount
  onMount(() => {
    const token = localStorage.getItem('authToken');
    if (token) {
      // Verify token with MiniApps API
      fetch('https://its.mouamle.space/api/auth-with-superQi', {
        method: 'POST',
        headers: {
          'Content-Type': 'application/json',
        },
        body: JSON.stringify({
          token: token
        })
      })
      .then(response => {
        if (response.ok) {
          return response.json();
        }
        throw new Error('Token invalid');
      })
      .then(data => {
        userInfo = data.user || data;
        isAuthenticated = true;
      })
      .catch(() => {
        localStorage.removeItem('authToken');
      });
    }
  });
  
  // Export functions for parent components
  export { getAuthCode, logout, isAuthenticated, userInfo };
</script>

{#if isAuthenticated}
  <div class="flex items-center space-x-4">
    <div class="flex items-center space-x-2">
      <div class="w-8 h-8 bg-red-600 rounded-full flex items-center justify-center text-white text-sm font-bold">
        {userInfo?.name?.[0]?.toUpperCase() || 'U'}
      </div>
      <span class="text-white text-sm">{userInfo?.name || 'User'}</span>
    </div>
    <button 
      on:click={logout}
      class="px-3 py-1 text-xs bg-gray-700 hover:bg-gray-600 text-white rounded transition-colors"
    >
      Logout
    </button>
  </div>
{:else}
  <button 
    on:click={getAuthCode}
    disabled={isLoading}
    class="px-6 py-3 bg-red-600 hover:bg-red-700 disabled:bg-gray-600 text-white rounded-lg font-medium transition-all duration-300 transform hover:scale-105 focus:outline-none focus:ring-2 focus:ring-red-500 focus:ring-opacity-50"
  >
    {#if isLoading}
      <span class="flex items-center">
        <svg class="animate-spin -ml-1 mr-3 h-5 w-5 text-white" xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 24 24">
          <circle class="opacity-25" cx="12" cy="12" r="10" stroke="currentColor" stroke-width="4"></circle>
          <path class="opacity-75" fill="currentColor" d="M4 12a8 8 0 018-8V0C5.373 0 0 5.373 0 12h4zm2 5.291A7.962 7.962 0 014 12H0c0 3.042 1.135 5.824 3 7.938l3-2.647z"></path>
        </svg>
        Authenticating...
      </span>
    {:else}
      Continue with Super App
    {/if}
  </button>
{/if}

{#if authError}
  <div class="mt-4 p-3 bg-red-900 bg-opacity-50 border border-red-700 rounded-lg">
    <p class="text-red-300 text-sm">{authError}</p>
  </div>
{/if}

<style>
  @keyframes spin {
    from {
      transform: rotate(0deg);
    }
    to {
      transform: rotate(360deg);
    }
  }
  
  .animate-spin {
    animation: spin 1s linear infinite;
  }
</style>
