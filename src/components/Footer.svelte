<script>
  const currentYear = new Date().getFullYear();

  const socialLinks = [
    {
      name: "Facebook",
      icon: "M24 12.073c0-6.627-5.373-12-12-12s-12 5.373-12 12c0 5.99 4.388 10.954 10.125 11.854v-8.385H7.078v-3.47h3.047V9.43c0-3.007 1.792-4.669 4.533-4.669 1.312 0 2.686.235 2.686.235v2.953H15.83c-1.491 0-1.956.925-1.956 1.874v2.25h3.328l-.532 3.47h-2.796v8.385C19.612 23.027 24 18.062 24 12.073z",
      url: "#",
    },
    {
      name: "Instagram",
      icon: "M12 2.163c3.204 0 3.584.012 4.85.07 3.252.148 4.771 1.691 4.919 4.919.058 1.265.069 1.645.069 4.849 0 3.205-.012 3.584-.069 4.849-.149 3.225-1.664 4.771-4.919 4.919-1.266.058-1.644.07-4.85.07-3.204 0-3.584-.012-4.849-.07-3.26-.149-4.771-1.699-4.919-4.92-.058-1.265-.07-1.644-.07-4.849 0-3.204.013-3.583.07-4.849.149-3.227 1.664-4.771 4.919-4.919 1.266-.057 1.645-.069 4.849-.069zM12 0C8.741 0 8.333.014 7.053.072 2.695.272.273 2.69.073 7.052.014 8.333 0 8.741 0 12c0 3.259.014 3.668.072 4.948.2 4.358 2.618 6.78 6.98 6.98C8.333 23.986 8.741 24 12 24c3.259 0 3.668-.014 4.948-.072 4.354-.2 6.782-2.618 6.979-6.98.059-1.28.073-1.689.073-4.948 0-3.259-.014-3.667-.072-4.947-.196-4.354-2.617-6.78-6.979-6.98C15.668.014 15.259 0 12 0zm0 5.838a6.162 6.162 0 100 12.324 6.162 6.162 0 000-12.324zM12 16a4 4 0 110-8 4 4 0 010 8zm6.406-11.845a1.44 1.44 0 100 2.881 1.44 1.44 0 000-2.881z",
      url: "#",
    },
    {
      name: "Twitter",
      icon: "M23.953 4.57a10 10 0 01-2.825.775 4.958 4.958 0 002.163-2.723c-.951.555-2.005.959-3.127 1.184a4.92 4.92 0 00-8.384 4.482C7.69 8.095 4.067 6.13 1.64 3.162a4.822 4.822 0 00-.666 2.475c0 1.71.87 3.213 2.188 4.096a4.904 4.904 0 01-2.228-.616v.06a4.923 4.923 0 003.946 4.827 4.996 4.996 0 01-2.212.085 4.936 4.936 0 004.604 3.417 9.867 9.867 0 01-6.102 2.105c-.39 0-.779-.023-1.17-.067a13.995 13.995 0 007.557 2.209c9.053 0 13.998-7.496 13.998-13.985 0-.21 0-.42-.015-.63A9.935 9.935 0 0024 4.59z",
      url: "#",
    },
    {
      name: "YouTube",
      icon: "M23.498 6.186a3.016 3.016 0 0 0-2.122-2.136C19.505 3.545 12 3.545 12 3.545s-7.505 0-9.377.505A3.017 3.017 0 0 0 .502 6.186C0 8.07 0 12 0 12s0 3.93.502 5.814a3.016 3.016 0 0 0 2.122 2.136c1.871.505 9.376.505 9.376.505s7.505 0 9.377-.505a3.015 3.015 0 0 0 2.122-2.136C24 15.93 24 12 24 12s0-3.93-.502-5.814zM9.545 15.568V8.432L15.818 12l-6.273 3.568z",
      url: "#",
    },
  ];
</script>

<footer
  class="bg-black border-t border-gray-800 border-opacity-50 pt-16 md:pt-20 pb-12 relative overflow-hidden"
>
  <!-- Background Effects -->
  <div class="absolute inset-0">
    <div
      class="absolute top-0 left-0 w-96 h-96 bg-red-600 rounded-full filter blur-3xl opacity-5 animate-pulse-slow"
    ></div>
    <div
      class="absolute bottom-0 right-0 w-96 h-96 bg-red-500 rounded-full filter blur-3xl opacity-5 animate-pulse-slow"
      style="animation-delay: 3s;"
    ></div>
  </div>

  <div class="container-custom max-w-7xl mx-auto relative z-10">
    <div class="flex flex-col items-center text-center">
      <!-- Logo and Description -->
      <div class="mb-10 max-w-2xl">
        <div class="flex items-center justify-center mb-6">
          <div
            class="w-12 h-12 bg-gradient-to-br from-red-600 to-red-800 rounded-2xl flex items-center justify-center text-white shadow-xl shadow-glow mr-4"
          >
            <svg
              xmlns="http://www.w3.org/2000/svg"
              class="h-7 w-7"
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
          <span class="text-3xl font-black text-white">INFINITY GYM</span>
        </div>
        <p class="text-gray-400 mb-8 text-lg leading-relaxed">
          Helping you achieve your fitness goals with state-of-the-art
          facilities and expert trainers.
        </p>

        <div class="flex justify-center space-x-8 mb-12">
          {#each socialLinks as social}
            <a
              href={social.url}
              target="_blank"
              rel="noopener noreferrer"
              class="text-gray-400 hover:text-red-500 transition-all duration-300 hover:scale-110"
              aria-label={social.name}
            >
              <svg
                class="w-6 h-6"
                fill="currentColor"
                viewBox="0 0 24 24"
                aria-hidden="true"
              >
                <path fill-rule="evenodd" d={social.icon} clip-rule="evenodd" />
              </svg>
            </a>
          {/each}
        </div>
      </div>

      <!-- Copyright -->
      <div class="w-full border-t border-gray-800 border-opacity-50 pt-8">
        <div
          class="flex flex-col md:flex-row justify-between items-center text-sm md:text-base"
        >
          <p class="text-gray-500 mb-4 md:mb-0">
            &copy; {currentYear} Infinity Gym. All rights reserved.
          </p>
          <div class="flex space-x-6">
            <button
              class="text-gray-500 hover:text-red-500 transition-colors duration-200"
              aria-label="Privacy Policy">Privacy Policy</button
            >
            <button
              class="text-gray-500 hover:text-red-500 transition-colors duration-200"
              aria-label="Terms of Service">Terms of Service</button
            >
          </div>
        </div>
      </div>
    </div>
  </div>
</footer>
