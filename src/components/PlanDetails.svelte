<script>
    export let plan;
    export let onBack = () => {};
    export let onPay = () => {};
</script>

<div class="fixed inset-0 z-50 bg-black overflow-y-auto animate-fade-in-up">
    <!-- Background Effects -->
    <div class="fixed inset-0 pointer-events-none">
        <div
            class="absolute inset-0 bg-gradient-to-br from-red-900 via-gray-900 to-black opacity-40"
        ></div>
        <div
            class="absolute top-0 right-0 w-96 h-96 bg-red-600 rounded-full filter blur-3xl opacity-10 animate-pulse-slow"
        ></div>
        <div
            class="absolute bottom-0 left-0 w-96 h-96 bg-red-500 rounded-full filter blur-3xl opacity-10 animate-pulse-slow"
            style="animation-delay: 2s;"
        ></div>
    </div>

    <div class="container-custom relative z-10 py-8 min-h-screen flex flex-col">
        <!-- Header -->
        <div class="flex items-center justify-between mb-8">
            <button
                on:click={onBack}
                class="flex items-center text-gray-400 hover:text-white transition-colors group"
            >
                <svg
                    xmlns="http://www.w3.org/2000/svg"
                    class="h-6 w-6 mr-2 transform group-hover:-translate-x-1 transition-transform"
                    fill="none"
                    viewBox="0 0 24 24"
                    stroke="currentColor"
                >
                    <path
                        stroke-linecap="round"
                        stroke-linejoin="round"
                        stroke-width="2"
                        d="M15 19l-7-7 7-7"
                    />
                </svg>
                <span>Back to Plans</span>
            </button>

            <div class="text-white font-bold text-xl">Checkout</div>
        </div>

        <!-- Main Content -->
        <div class="flex-grow max-w-2xl mx-auto w-full">
            <div class="card-dark p-6 md:p-8 mb-8">
                <div class="text-center mb-8">
                    <h2
                        class="text-gray-400 uppercase tracking-widest text-sm font-semibold mb-2"
                    >
                        Selected Plan
                    </h2>
                    <h1
                        class="text-4xl md:text-5xl font-black text-white text-gradient mb-4"
                    >
                        {plan.name}
                    </h1>
                    <div class="flexItems-center justify-center">
                        <span class="text-5xl font-bold text-white"
                            >${plan.price}</span
                        >
                        <span class="text-xl text-gray-400 ml-2"
                            >/{plan.period}</span
                        >
                    </div>
                </div>

                <div class="border-t border-gray-700 my-8"></div>

                <div class="space-y-6">
                    <h3 class="text-xl font-bold text-white mb-4">
                        Plan Features
                    </h3>
                    <ul class="space-y-4">
                        {#each plan.features as feature}
                            <li class="flex items-start">
                                <div
                                    class="bg-green-500/10 p-1 rounded-full mr-4 mt-0.5"
                                >
                                    <svg
                                        class="h-5 w-5 text-green-500"
                                        fill="none"
                                        viewBox="0 0 24 24"
                                        stroke="currentColor"
                                    >
                                        <path
                                            stroke-linecap="round"
                                            stroke-linejoin="round"
                                            stroke-width="2"
                                            d="M5 13l4 4L19 7"
                                        />
                                    </svg>
                                </div>
                                <span class="text-gray-200 text-lg"
                                    >{feature}</span
                                >
                            </li>
                        {/each}
                    </ul>
                </div>

                <div
                    class="bg-gray-800/50 rounded-xl p-6 mt-10 border border-gray-700"
                >
                    <div class="flex justify-between items-center mb-2">
                        <span class="text-gray-400">Subtotal</span>
                        <span class="text-white text-lg">${plan.price}</span>
                    </div>
                    <div class="flex justify-between items-center mb-4">
                        <span class="text-gray-400">Tax</span>
                        <span class="text-white text-lg">$0.00</span>
                    </div>
                    <div class="border-t border-gray-600 my-4"></div>
                    <div class="flex justify-between items-center">
                        <span class="text-xl font-bold text-white">Total</span>
                        <span class="text-3xl font-black text-white"
                            >${plan.price}</span
                        >
                    </div>
                </div>
            </div>
        </div>

        <!-- Footer / Pay Button -->
        <div
            class="max-w-2xl mx-auto w-full sticky bottom-0 bg-gradient-to-t from-black via-black to-transparent pt-8 pb-8"
        >
            <button
                on:click={() => onPay(plan)}
                class="w-full btn-primary py-5 text-xl font-bold shadow-glow hover:shadow-glow-lg flex items-center justify-center gap-3 transform hover:-translate-y-1 transition-all"
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
                        d="M17 9V7a2 2 0 00-2-2H5a2 2 0 00-2 2v6a2 2 0 002 2h2m2 4h10a2 2 0 002-2v-6a2 2 0 00-2-2H9a2 2 0 00-2 2v6a2 2 0 002 2zm7-5a2 2 0 11-4 0 2 2 0 014 0z"
                    />
                </svg>
                Pay Now
            </button>
            <p class="text-center text-gray-500 text-sm mt-4">
                Safe & Secure Payment
            </p>
        </div>
    </div>
</div>
