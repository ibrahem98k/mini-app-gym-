<script>
    import { onMount } from "svelte";
    import { fade, fly } from "svelte/transition";
    import SubscriptionStatus from "../../components/SubscriptionStatus.svelte";
    import { goto } from "$app/navigation";

    let hasSubscription = false;
    let isLoading = true;

    // Default empty subscription for when none exists
    let subscriptionData = {
        active: false,
        plan: null,
        startDate: null,
        endDate: null,
        daysLeft: 0,
        totalDays: 0,
        visitsUsed: 0,
        totalVisits: 0,
        status: "inactive",
    };

    onMount(() => {
        // Simulate loading data
        setTimeout(() => {
            const savedSubscription = localStorage.getItem("gymSubscription");
            if (savedSubscription) {
                try {
                    subscriptionData = JSON.parse(savedSubscription);
                    hasSubscription = true;
                } catch (e) {
                    console.error("Failed to parse subscription data", e);
                }
            }
            isLoading = false;
        }, 800);
    });
</script>

<div
    class="min-h-screen bg-black pt-20 pb-12 px-4 relative overflow-hidden flex flex-col items-center justify-center"
>
    <!-- Background Effects -->
    <div class="absolute inset-0 pointer-events-none">
        <div
            class="absolute inset-0 bg-gradient-to-b from-gray-950 via-gray-900 to-black"
        ></div>
        <!-- Animated accent orbs -->
        <div
            class="absolute top-0 right-1/4 w-[500px] h-[500px] bg-red-600/10 rounded-full blur-[100px] animate-pulse"
        ></div>
        <div
            class="absolute bottom-0 left-1/4 w-[500px] h-[500px] bg-gray-600/10 rounded-full blur-[100px] animate-pulse"
            style="animation-delay: 2s"
        ></div>
        <!-- Grid pattern overlay removed -->
    </div>

    <div class="container-custom relative z-10 max-w-lg w-full mb-auto mt-8">
        <button
            on:click={() => goto("/")}
            class="group flex items-center gap-2 mb-8 text-sm font-medium text-gray-400 hover:text-white transition-all duration-300 hover:pl-2 px-4 py-2 rounded-full hover:bg-white/5 w-fit"
        >
            <div
                class="w-8 h-8 rounded-full bg-gray-800 flex items-center justify-center border border-gray-700 group-hover:border-red-500/50 group-hover:bg-red-500/10 transition-colors"
            >
                <svg
                    xmlns="http://www.w3.org/2000/svg"
                    class="h-4 w-4 transition-transform group-hover:-translate-x-0.5"
                    fill="none"
                    viewBox="0 0 24 24"
                    stroke="currentColor"
                >
                    <path
                        stroke-linecap="round"
                        stroke-linejoin="round"
                        stroke-width="2"
                        d="M10 19l-7-7m0 0l7-7m-7 7h18"
                    />
                </svg>
            </div>
            <span>Back to Home</span>
        </button>

        <div class="text-center mb-10">
            <h1
                class="text-4xl md:text-5xl font-black text-white mb-2 tracking-tight"
            >
                Subscription <span
                    class="text-transparent bg-clip-text bg-gradient-to-r from-red-500 to-orange-600"
                    >Status</span
                >
            </h1>
            <p class="text-gray-400">Manage your active plan and details</p>
        </div>

        {#if isLoading}
            <div
                class="flex flex-col items-center justify-center py-12 bg-gray-900/40 backdrop-blur-md rounded-2xl border border-gray-800/50"
                in:fade
            >
                <div class="relative w-16 h-16 mb-6">
                    <div
                        class="absolute inset-0 border-4 border-gray-700/50 rounded-full"
                    ></div>
                    <div
                        class="absolute inset-0 border-4 border-red-600 border-t-transparent rounded-full animate-spin"
                    ></div>
                </div>
                <p
                    class="text-gray-400 animate-pulse font-medium tracking-wide"
                >
                    SYNCING MEMBER DATA...
                </p>
            </div>
        {:else}
            <div in:fly={{ y: 20, duration: 600, delay: 100 }}>
                <SubscriptionStatus subscription={subscriptionData} />

                {#if !hasSubscription}
                    <div class="mt-8 text-center" in:fade={{ delay: 300 }}>
                        <p class="text-gray-500 mb-6 text-sm">
                            Ready to take your fitness to the next level?
                        </p>
                        <button
                            on:click={() => goto("/#plans")}
                            class="inline-flex items-center gap-2 bg-gradient-to-r from-red-600 to-red-500 text-white px-8 py-3 rounded-full font-bold shadow-lg shadow-red-500/25 hover:shadow-red-500/40 hover:scale-[1.02] active:scale-[0.98] transition-all duration-300"
                        >
                            <span>Browse Plans</span>
                            <svg
                                xmlns="http://www.w3.org/2000/svg"
                                class="h-5 w-5"
                                fill="none"
                                viewBox="0 0 24 24"
                                stroke="currentColor"
                            >
                                <path
                                    stroke-linecap="round"
                                    stroke-linejoin="round"
                                    stroke-width="2"
                                    d="M17 8l4 4m0 0l-4 4m4-4H3"
                                />
                            </svg>
                        </button>
                    </div>
                {/if}
            </div>
        {/if}
    </div>

    <div class="text-center py-6 text-gray-600 text-sm">
        &copy; {new Date().getFullYear()} GymBrand. All rights reserved.
    </div>
</div>
