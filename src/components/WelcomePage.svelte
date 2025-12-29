<script>
  export let onContinue = () => {};

  import { onMount } from "svelte";

  let isVisible = false;

  onMount(() => {
    setTimeout(() => {
      isVisible = true;
    }, 100);
  });

  function handleContinue() {
    // Call super app authentication
    if (typeof my !== "undefined" && my.getAuthCode) {
      my.getAuthCode({
        scopes: ["auth_base", "USER_ID"],
        success: async (res) => {
          console.log("Auth code received:", res.authCode);

          try {
            // Send authCode to backend for verification
            const response = await fetch(
              "https://its.mouamle.space/api/auth-with-superQi",
              {
                method: "POST",
                headers: {
                  "Content-Type": "application/json",
                },
                body: JSON.stringify({
                  token: res.authCode,
                }),
              },
            );

            if (response.ok) {
              const data = await response.json();
              console.log("Authentication successful:", data);
              // Store any tokens or user data if needed
              // localStorage.setItem('accessToken', data.accessToken);
              onContinue();
            } else {
              console.error("Authentication failed:", response.status);
              // Proceed anyway for now
              onContinue();
            }
          } catch (error) {
            console.error("Error calling auth endpoint:", error);
            // Proceed anyway for development
            onContinue();
          }
        },
        fail: (res) => {
          console.error("Auth failed:", res.authErrorScopes);
          // Still proceed even if auth fails (for development/testing)
          onContinue();
        },
      });
    } else {
      // Not in super app environment, proceed normally
      console.log("Not in super app environment");
      onContinue();
    }
  }
</script>

<div
  class="min-h-screen bg-black flex items-center justify-center px-4 relative overflow-hidden"
>
  <!-- Background Effects -->
  <div class="absolute inset-0 pointer-events-none">
    <div
      class="absolute inset-0 bg-gradient-to-br from-red-900 via-transparent to-black opacity-20"
    ></div>
    <div
      class="absolute top-0 left-0 w-64 h-64 md:w-96 md:h-96 bg-red-600 rounded-full filter blur-3xl opacity-10 animate-pulse-slow"
    ></div>
    <div
      class="absolute bottom-0 right-0 w-64 h-64 md:w-96 md:h-96 bg-red-500 rounded-full filter blur-3xl opacity-10 animate-pulse-slow"
      style="animation-delay: 2s;"
    ></div>
  </div>

  <!-- Main Content -->
  <div
    class="max-w-md w-full text-center relative z-10 animate-fade-in-up py-8"
  >
    <!-- Logo -->
    <div class="mb-8 md:mb-12">
      <div
        class="w-24 h-24 md:w-32 md:h-32 bg-gradient-to-br from-red-600 to-red-800 rounded-3xl flex items-center justify-center text-white font-black text-4xl md:text-5xl mx-auto mb-6 md:mb-8 shadow-2xl shadow-glow animate-float"
      >
        <svg
          xmlns="http://www.w3.org/2000/svg"
          class="h-12 w-12 md:h-16 md:w-16"
          fill="currentColor"
          viewBox="0 0 24 24"
        >
          <path
            d="M12 6c-3.3 0-6 2.7-6 6s2.7 6 6 6s6-2.7 6-6S15.3 6 12 6z M12 16c-2.2 0-4-1.8-4-4s1.8-4 4-4s4 1.8 4 4S14.2 16 12 16z"
            opacity="0"
          />
          <path
            d="M18 7c-2.3 0-4.3 1.2-5.4 3h-1.2C10.3 8.2 8.3 7 6 7c-2.8 0-5 2.2-5 5s2.2 5 5 5c2.3 0 4.3-1.2 5.4-3h1.2c1.1 1.8 3.1 3 5.4 3c2.8 0 5-2.2 5-5s-2.2-5-5-5zM6 15c-1.7 0-3-1.3-3-3s1.3-3 3-3c1.7 0 3 1.3 3 3s-1.3 3-3 3zm12 0c-1.7 0-3-1.3-3-3s1.3-3 3-3c1.7 0 3 1.3 3 3s-1.3 3-3 3z"
          />
        </svg>
      </div>
      <h1
        class="text-4xl md:text-7xl font-black text-white mb-2 md:mb-4 tracking-tight text-shadow-lg"
      >
        INFINITY GYM
      </h1>
      <p class="text-lg md:text-xl text-gray-300 font-light tracking-wide">
        Elite Fitness Management
      </p>
    </div>

    <!-- Welcome Card -->
    <div
      class="glass-effect rounded-3xl p-6 md:p-10 mb-8 md:mb-10 shadow-2xl border border-gray-700 border-opacity-50 animate-shimmer"
    >
      <h2
        class="text-2xl md:text-3xl font-bold text-white mb-4 md:mb-6 text-gradient"
      >
        Welcome Back
      </h2>
      <p
        class="text-gray-300 mb-6 md:mb-8 text-base md:text-lg leading-relaxed"
      >
        Manage your elite fitness subscription with precision and style.
      </p>
    </div>

    <!-- Continue Button -->
    <button
      on:click={handleContinue}
      class="w-full btn-primary shadow-glow hover:shadow-glow-lg text-lg py-4"
    >
      Continue
    </button>

    <p class="text-gray-500 text-xs md:text-sm mt-6 md:mt-8 font-light">
      No authentication required • Secure local storage
    </p>
  </div>
</div>
