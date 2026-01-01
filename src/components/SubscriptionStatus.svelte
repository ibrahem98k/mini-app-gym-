<script>
  import { fade, slide } from "svelte/transition";

  export let subscription = {
    active: false,
    plan: null,
    startDate: null,
    endDate: null,
    daysLeft: 0,
  };

  $: progress =
    subscription.daysLeft > 0
      ? Math.max(0, Math.min(100, (subscription.daysLeft / 30) * 100))
      : 0;

  $: statusColor = {
    active: "bg-emerald-500 shadow-[0_0_15px_rgba(16,185,129,0.6)]",
    expired: "bg-red-500 shadow-[0_0_15px_rgba(239,68,68,0.6)]",
    inactive: "bg-gray-500 shadow-[0_0_15px_rgba(107,114,128,0.6)]",
  }[subscription.active ? "active" : "inactive"];

  $: statusText = subscription.active ? "Active Membership" : "Inactive";

  // Format date helper
  const formatDate = (dateString) => {
    if (!dateString) return "-";
    return new Date(dateString).toLocaleDateString("en-US", {
      year: "numeric",
      month: "short",
      day: "numeric",
    });
  };
</script>

<div class="relative w-full max-w-md mx-auto group perspective-1000">
  <!-- Main Card -->
  <div
    class="relative overflow-hidden bg-gray-900/60 backdrop-blur-xl rounded-3xl border border-gray-800/60 shadow-2xl transition-all duration-500 hover:border-gray-700/80 hover:shadow-red-900/20"
  >
    <!-- Ambient Background Glows -->
    <div
      class="absolute top-0 right-0 w-64 h-64 bg-red-600/5 rounded-full blur-[80px] -mr-16 -mt-16 pointer-events-none"
    ></div>
    <div
      class="absolute bottom-0 left-0 w-64 h-64 bg-blue-600/5 rounded-full blur-[80px] -ml-16 -mb-16 pointer-events-none"
    ></div>

    <!-- Header Section -->
    <div class="p-6 border-b border-gray-800/50 bg-black/20">
      <div class="flex items-center justify-between">
        <div class="flex items-center gap-3">
          <div
            class="p-2 bg-gray-800/80 rounded-xl border border-gray-700/50 shadow-inner"
          >
            <svg
              xmlns="http://www.w3.org/2000/svg"
              class="h-6 w-6 text-gray-200"
              fill="none"
              viewBox="0 0 24 24"
              stroke="currentColor"
            >
              <path
                stroke-linecap="round"
                stroke-linejoin="round"
                stroke-width="2"
                d="M10 6H5a2 2 0 00-2 2v9a2 2 0 002 2h14a2 2 0 002-2V8a2 2 0 00-2-2h-5m-4 0V5a2 2 0 114 0v1m-4 0a2 2 0 104 0m-5 8a2 2 0 100-4 2 2 0 000 4zm0 0c1.306 0 2.417.835 2.83 2M9 14a3.001 3.001 0 00-2.83 2M15 11h3m-3 4h2"
              />
            </svg>
          </div>
          <div>
            <h2 class="text-lg font-bold text-white leading-tight">
              Member Card
            </h2>
            <p class="text-xs text-gray-400 font-medium">Digital Pass</p>
          </div>
        </div>

        <div
          class="flex items-center gap-2 bg-gray-950/50 pl-2 pr-3 py-1.5 rounded-full border border-gray-800"
        >
          <span class="relative flex h-2.5 w-2.5">
            <span
              class="animate-ping absolute inline-flex h-full w-full rounded-full opacity-75 {statusColor.split(
                ' ',
              )[0]}"
            ></span>
            <span
              class="relative inline-flex rounded-full h-2.5 w-2.5 {statusColor}"
            ></span>
          </span>
          <span class="text-gray-200 text-xs font-bold tracking-wide uppercase"
            >{statusText}</span
          >
        </div>
      </div>
    </div>

    <!-- Content Section -->
    <div class="p-6">
      {#if subscription.active}
        <div in:slide|local>
          <!-- Plan Name -->
          <div class="mb-8">
            <p
              class="text-xs text-gray-500 font-semibold uppercase tracking-wider mb-2"
            >
              Current Plan
            </p>
            <h3
              class="text-3xl font-black text-transparent bg-clip-text bg-gradient-to-r from-white via-gray-100 to-gray-400"
            >
              {subscription.plan?.name || "Premium Access"}
            </h3>
          </div>

          <!-- Progress Bar -->
          <div class="mb-8">
            <div class="flex justify-between items-end mb-2">
              <span class="text-sm font-medium text-gray-400">Remaining</span>
              <div class="flex items-baseline gap-1">
                <span class="text-2xl font-bold text-white"
                  >{subscription.daysLeft}</span
                >
                <span class="text-xs text-gray-500 font-medium uppercase"
                  >Days</span
                >
              </div>
            </div>

            <div class="h-2 w-full bg-gray-800 rounded-full overflow-hidden">
              <div
                class="h-full bg-gradient-to-r from-red-600 to-orange-500 rounded-full relative"
                style="width: {progress}%"
              >
                <div
                  class="absolute top-0 right-0 bottom-0 w-[1px] bg-white/50 shadow-[0_0_10px_white]"
                ></div>
              </div>
            </div>
          </div>

          <!-- Info Grid -->
          <div class="grid grid-cols-2 gap-4 mb-8">
            <div
              class="bg-gray-800/30 p-4 rounded-2xl border border-gray-700/30"
            >
              <p class="text-xs text-gray-500 mb-1">Start Date</p>
              <p class="text-white font-semibold">
                {formatDate(subscription.startDate)}
              </p>
            </div>
            <div
              class="bg-gray-800/30 p-4 rounded-2xl border border-gray-700/30"
            >
              <p class="text-xs text-gray-500 mb-1">End Date</p>
              <p class="text-white font-semibold">
                {formatDate(subscription.endDate)}
              </p>
            </div>
          </div>
        </div>
      {:else}
        <div class="py-6 text-center" in:fade>
          <div class="mb-6 relative inline-block">
            <div
              class="absolute inset-0 bg-red-500/20 blur-xl rounded-full animate-pulse"
            ></div>
            <div
              class="relative bg-gray-800 rounded-full p-4 border border-gray-700"
            >
              <svg
                xmlns="http://www.w3.org/2000/svg"
                class="h-8 w-8 text-gray-400"
                fill="none"
                viewBox="0 0 24 24"
                stroke="currentColor"
              >
                <path
                  stroke-linecap="round"
                  stroke-linejoin="round"
                  stroke-width="2"
                  d="M12 15v2m-6 4h12a2 2 0 002-2v-6a2 2 0 00-2-2H6a2 2 0 00-2 2v6a2 2 0 002 2zm10-10V7a4 4 0 00-8 0v4h8z"
                />
              </svg>
            </div>
          </div>

          <h3 class="text-xl font-bold text-white mb-2">
            No Active Subscription
          </h3>
          <p class="text-gray-400 text-sm mb-8 leading-relaxed px-4">
            Your fitness journey is waiting. Activate your premium membership
            today.
          </p>

          <a
            href="/plans"
            class="block w-full bg-gradient-to-r from-red-600 to-red-500 text-white font-bold py-3.5 rounded-xl shadow-lg shadow-red-900/20 hover:shadow-red-600/30 transition-all hover:-translate-y-0.5 text-center"
          >
            View Membership Plans
          </a>
        </div>
      {/if}
    </div>
  </div>
</div>
