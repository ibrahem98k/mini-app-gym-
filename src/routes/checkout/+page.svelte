<script>
    import { page } from "$app/stores";
    import { onMount } from "svelte";

    let planId = "";
    let selectedPlan = null;

    const plans = [
        { id: "monthly", name: "Monthly", price: "49" },
        { id: "quarterly", name: "Quarterly", price: "129" },
        { id: "yearly", name: "Yearly", price: "399" },
    ];

    onMount(() => {
        window.scrollTo(0, 0);
        planId = $page.url.searchParams.get("plan");
        selectedPlan = plans.find((p) => p.id === planId);
    });
</script>

<div class="min-h-screen bg-gray-900 pt-24 px-4">
    <div
        class="max-w-2xl mx-auto bg-gray-800 rounded-2xl p-8 shadow-xl border border-gray-700"
    >
        <h1 class="text-3xl font-black text-white mb-6">Checkout</h1>

        {#if selectedPlan}
            <div
                class="bg-gray-700/50 p-6 rounded-xl border border-gray-600 mb-8"
            >
                <h2 class="text-xl font-bold text-white mb-2">Selected Plan</h2>
                <div class="flex justify-between items-center">
                    <div>
                        <p class="text-white text-lg font-bold">
                            {selectedPlan.name}
                        </p>
                        <p class="text-gray-400">Gym Membership</p>
                    </div>
                    <p class="text-2xl font-black text-white">
                        ${selectedPlan.price}
                    </p>
                </div>
            </div>

            <div class="mt-8">
                <button
                    class="w-full bg-gradient-to-r from-red-600 to-red-700 text-white font-bold text-lg py-4 rounded-xl hover:from-red-700 hover:to-red-800 transition-all duration-200 shadow-lg shadow-red-900/40"
                >
                    Pay ${selectedPlan.price}
                </button>
            </div>
        {:else}
            <div class="text-center py-12">
                <p class="text-gray-400 mb-4">No plan selected</p>
                <a
                    href="/#plans"
                    class="text-red-500 hover:text-red-400 font-bold"
                    >Go back to plans</a
                >
            </div>
        {/if}
    </div>
</div>
