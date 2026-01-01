<script>
  import { goto } from "$app/navigation";

  export let title = "Elite Fitness Management";
  export let subtitle =
    "Track your subscription, manage plans, and achieve your fitness goals with precision and style.";

  let isScanning = false;

  const handleScanQR = () => {
    // Use super app's scan API if available
    if (typeof my !== "undefined" && my.scan) {
      isScanning = true;

      my.scan({
        type: "qr",
        success: (res) => {
          console.log("QR Code scanned:", res.code);
          isScanning = false;
          // Navigate to subscription status page
          goto("/status");
        },
        fail: (error) => {
          console.error("Scan failed:", error);
          isScanning = false;
        },
      });
    } else {
      // Fallback for development environment (not in super app)
      console.log("Not in super app environment - simulating scan");
      isScanning = true;
      setTimeout(() => {
        isScanning = false;
        goto("/status");
      }, 1500);
    }
  };

  const scrollToSection = (sectionId) => {
    const element = document.getElementById(sectionId);
    if (element) {
      element.scrollIntoView({ behavior: "smooth" });
    }
  };
</script>

<section
  id="home"
  class="section-padding bg-black text-white relative overflow-hidden"
>
  <!-- Background Effects -->
  <div class="absolute inset-0 pointer-events-none">
    <div
      class="absolute inset-0 bg-gradient-to-br from-red-900 via-transparent to-black opacity-30"
    ></div>
    <div
      class="absolute top-10 left-10 md:top-20 md:left-20 w-32 h-32 md:w-48 md:h-48 bg-red-600 rounded-full filter blur-3xl opacity-20 animate-pulse-slow"
    ></div>
    <div
      class="absolute bottom-10 right-10 md:bottom-20 md:right-20 w-32 h-32 md:w-48 md:h-48 bg-red-500 rounded-full filter blur-3xl opacity-20 animate-pulse-slow"
      style="animation-delay: 3s;"
    ></div>
  </div>

  <div class="container-custom relative z-10">
    <div class="max-w-5xl mx-auto text-center">
      <h1
        class="text-4xl md:text-6xl lg:text-7xl font-black mb-6 tracking-tight text-shadow-lg animate-fade-in-up leading-tight"
      >
        <span class="text-gradient block md:inline">{title}</span>
      </h1>
      <p
        class="text-lg md:text-2xl mb-10 md:mb-12 text-gray-300 font-light leading-relaxed max-w-4xl mx-auto animate-fade-in-up"
        style="animation-delay: 0.2s;"
      >
        {subtitle}
      </p>
      <div
        class="flex flex-col sm:flex-row justify-center gap-4 md:gap-6 animate-fade-in-up"
        style="animation-delay: 0.4s;"
      >
        <button
          on:click={() => goto("/plans")}
          class="btn-primary shadow-glow hover:shadow-glow-lg text-lg w-full sm:w-auto text-center"
        >
          View Plans
        </button>
        <button
          on:click={handleScanQR}
          class="border-3 border-red-600 text-red-500 hover:bg-red-600 hover:text-white font-bold py-4 px-8 rounded-2xl text-lg transition-all duration-300 shadow-xl hover:shadow-2xl transform hover:-translate-y-1 hover:scale-105 w-full sm:w-auto flex items-center justify-center gap-2"
        >
          <svg
            xmlns="http://www.w3.org/2000/svg"
            class="h-6 w-6"
            fill="none"
            viewBox="0 0 24 24"
            stroke="currentColor"
          >
            <path
              stroke-linecap="round"
              stroke-linejoin="round"
              stroke-width="2"
              d="M12 4v1m6 11h2m-6 0h-2v4m0-11v3m0 0h.01M12 12h4.01M16 20h4M4 12h4m12 0h.01M5 8h2a1 1 0 001-1V5a1 1 0 00-1-1H5a1 1 0 00-1 1v2a1 1 0 001 1zm12 0h2a1 1 0 001-1V5a1 1 0 00-1-1h-2a1 1 0 00-1 1v2a1 1 0 001 1zM5 20h2a1 1 0 001-1v-2a1 1 0 00-1-1H5a1 1 0 00-1 1v2a1 1 0 001 1z"
            />
          </svg>
          {isScanning ? "Scanning..." : "Scan QR Code"}
        </button>
      </div>
    </div>
  </div>
</section>
