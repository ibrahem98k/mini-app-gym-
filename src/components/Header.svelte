<script>
  import Auth from "./Auth.svelte";

  let menuOpen = false;

  const toggleMenu = () => {
    menuOpen = !menuOpen;
  };

  const scrollToSection = (sectionId) => {
    const element = document.getElementById(sectionId);
    if (element) {
      element.scrollIntoView({ behavior: "smooth" });
    }
    menuOpen = false;
  };
</script>

<header
  class="glass-effect sticky top-0 z-50 border-b border-gray-800 border-opacity-50"
>
  <div class="container-custom py-4 md:py-6">
    <div class="flex justify-between items-center">
      <!-- Logo with better touch target -->
      <a href="/" class="flex items-center space-x-3 md:space-x-4 p-2 -ml-2">
        <div
          class="w-10 h-10 md:w-12 md:h-12 bg-gradient-to-br from-red-600 to-red-800 rounded-2xl flex items-center justify-center text-white shadow-xl shadow-glow"
        >
          <svg
            xmlns="http://www.w3.org/2000/svg"
            class="h-5 w-5 md:h-7 md:w-7"
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
        <span class="text-2xl md:text-3xl font-black text-white tracking-tight"
          >INFINITY GYM</span
        >
      </a>

      <!-- Desktop Navigation with better spacing -->
      <nav class="hidden md:flex items-center space-x-8 lg:space-x-12">
        <button
          on:click={() => scrollToSection("home")}
          class="px-3 py-2 text-red-500 font-bold hover:text-red-400 transition-all duration-300 hover:scale-105 focus:outline-none focus:ring-2 focus:ring-red-500 focus:ring-opacity-50 rounded-lg"
          >Home</button
        >
        <button
          on:click={() => scrollToSection("plans")}
          class="px-3 py-2 text-gray-300 hover:text-red-500 transition-all duration-300 hover:scale-105 focus:outline-none focus:ring-2 focus:ring-red-500 focus:ring-opacity-50 rounded-lg"
          >Plans</button
        >
        <button
          on:click={() => scrollToSection("about")}
          class="px-3 py-2 text-gray-300 hover:text-red-500 transition-all duration-300 hover:scale-105 focus:outline-none focus:ring-2 focus:ring-red-500 focus:ring-opacity-50 rounded-lg"
          >About</button
        >
        <button
          on:click={() => scrollToSection("contact")}
          class="px-3 py-2 text-gray-300 hover:text-red-500 transition-all duration-300 hover:scale-105 focus:outline-none focus:ring-2 focus:ring-red-500 focus:ring-opacity-50 rounded-lg"
          >Contact</button
        >
        <!-- <Auth /> -->
      </nav>

      <!-- Enhanced mobile menu button -->
      <button
        class="md:hidden p-3 -mr-2 text-gray-300 hover:text-red-500 focus:outline-none transition-all duration-200 active:bg-gray-800 active:bg-opacity-30 rounded-full"
        on:click={toggleMenu}
        aria-label="Toggle menu"
        aria-expanded={menuOpen}
        aria-controls="mobile-menu"
      >
        <svg
          class="w-6 h-6"
          fill="none"
          stroke="currentColor"
          viewBox="0 0 24 24"
          xmlns="http://www.w3.org/2000/svg"
        >
          {#if menuOpen}
            <path
              stroke-linecap="round"
              stroke-linejoin="round"
              stroke-width="2"
              d="M6 18L18 6M6 6l12 12"
            />
          {:else}
            <path
              stroke-linecap="round"
              stroke-linejoin="round"
              stroke-width="2"
              d="M4 6h16M4 12h16m-7 6h7"
            />
          {/if}
        </svg>
      </button>
    </div>

    <!-- Enhanced Mobile Menu with better animations -->
    <div
      id="mobile-menu"
      class="mobile-menu md:hidden overflow-hidden transition-all duration-300 ease-in-out {menuOpen
        ? 'open'
        : ''}"
      style="max-height: {menuOpen ? '500px' : '0'}; opacity: {menuOpen
        ? '1'
        : '0'}"
    >
      <div class="pt-4 pb-6 border-t border-gray-800 border-opacity-50">
        <button
          on:click={() => scrollToSection("home")}
          class="block w-full px-4 py-3 text-left text-lg font-medium text-red-500 hover:bg-gray-800 hover:bg-opacity-30 rounded-lg transition-colors duration-200"
        >
          Home
        </button>
        <button
          on:click={() => scrollToSection("plans")}
          class="block w-full px-4 py-3 text-left text-lg font-medium text-gray-300 hover:text-red-500 hover:bg-gray-800 hover:bg-opacity-30 rounded-lg transition-colors duration-200"
        >
          Plans
        </button>
        <button
          on:click={() => scrollToSection("about")}
          class="block w-full px-4 py-3 text-left text-lg font-medium text-gray-300 hover:text-red-500 hover:bg-gray-800 hover:bg-opacity-30 rounded-lg transition-colors duration-200"
        >
          About
        </button>
        <button
          on:click={() => scrollToSection("contact")}
          class="block w-full px-4 py-3 text-left text-lg font-medium text-gray-300 hover:text-red-500 hover:bg-gray-800 hover:bg-opacity-30 rounded-lg transition-colors duration-200"
        >
          Contact
        </button>
        <div class="mt-4 pt-4 border-t border-gray-800 border-opacity-50">
          <!-- <Auth /> -->
        </div>
      </div>
    </div>
  </div>
</header>
