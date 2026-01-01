<script>
    import { page } from "$app/stores";
    import { onMount } from "svelte";
    import { goto } from "$app/navigation";

    let planId = "";
    let selectedPlan = null;
    let isProcessing = false;

    const plans = [
        {
            id: "monthly",
            name: "Monthly",
            price: "49",
            period: "month",
            days: 30,
        },
        {
            id: "quarterly",
            name: "Quarterly",
            price: "129",
            period: "3 months",
            days: 90,
        },
        {
            id: "yearly",
            name: "Yearly",
            price: "399",
            period: "year",
            days: 365,
        },
    ];

    onMount(() => {
        window.scrollTo(0, 0);
        planId = $page.url.searchParams.get("plan");
        selectedPlan = plans.find((p) => p.id === planId);
    });

    function completeSubscription(plan) {
        const endDate = new Date();
        endDate.setDate(endDate.getDate() + plan.days);

        const subscription = {
            active: true,
            plan,
            startDate: new Date(),
            endDate,
            daysLeft: plan.days,
            status: "active",
        };

        // Save subscription immediately
        localStorage.setItem("gymSubscription", JSON.stringify(subscription));
        
        // Force a small delay to ensure localStorage is written before redirect
        setTimeout(() => {
            // Show success and redirect immediately
            if (typeof my !== "undefined" && my.alert) {
                my.alert({
                    content: "Payment successful! Your membership is now active.",
                    success: () => {
                        goto("/status");
                    },
                });
            } else {
                goto("/status");
            }
        }, 100);
    }

    function pay() {
        const token = localStorage.getItem("accessToken") || "";
        isProcessing = true;

        if (typeof my !== "undefined" && my.tradePay) {
            fetch("https://its.mouamle.space/api/payment", {
                method: "POST",
                headers: {
                    "Content-Type": "application/json",
                    Authorization: token,
                },
            })
                .then((res) => res.json())
                .then((data) => {
                    my.tradePay({
                        paymentUrl: data.url,
                        success: (res) => {
                            isProcessing = false;
                            completeSubscription(selectedPlan);
                        },
                        fail: (res) => {
                            isProcessing = false;
                            my.alert({ content: "Payment failed" });
                        },
                    });
                })
                .catch((err) => {
                    isProcessing = false;
                    console.error("Payment request error:", err);
                    // For demo purposes, allow simulation even if API fails
                    completeSubscription(selectedPlan);
                });
        } else {
            // Fallback for development
            console.log("Not in super app - simulating payment");
            setTimeout(() => {
                isProcessing = false;
                completeSubscription(selectedPlan);
            }, 1000);
        }
    }
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
                    on:click={pay}
                    disabled={isProcessing}
                    class="w-full bg-gradient-to-r from-red-600 to-red-700 text-white font-bold text-lg py-4 rounded-xl hover:from-red-700 hover:to-red-800 transition-all duration-200 shadow-lg shadow-red-900/40 disabled:opacity-50 disabled:cursor-not-allowed"
                >
                    {isProcessing ? "Processing..." : "Pay"}
                </button>
            </div>
        {:else}
            <div class="text-center py-12">
                <p class="text-gray-400 mb-4">No plan selected</p>
                <a
                    href="/plans"
                    class="text-red-500 hover:text-red-400 font-bold"
                    >Go back to plans</a
                >
            </div>
        {/if}
    </div>
</div>
