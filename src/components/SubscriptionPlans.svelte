<script>
  export let activePlan = null;
  export let onSelectPlan = () => {};

  const plans = [
    {
      id: "monthly",
      name: "Monthly",
      price: "49",
      period: "month",
      popular: false,
      features: [
        "Access to all gym facilities",
        "Group fitness classes",
        "Locker room access",
        "Free WiFi",
        "1 Free Personal Training Session",
      ],
    },
    {
      id: "quarterly",
      name: "Quarterly",
      price: "129",
      period: "3 months",
      popular: true,
      features: [
        "Everything in Monthly",
        "Save 12%",
        "2 Free Personal Training Sessions",
        "Towel Service",
        "1 Free Guest Pass",
      ],
    },
    {
      id: "yearly",
      name: "Yearly",
      price: "399",
      period: "year",
      popular: false,
      features: [
        "Everything in Quarterly",
        "Save 32%",
        "6 Free Personal Training Sessions",
        "Sauna & Steam Room Access",
        "4 Free Guest Passes",
        "Nutrition Consultation",
      ],
    },
  ];

  function handleSubscribe(plan) {
    onSelectPlan(plan);
  }
</script>

<div id="plans" class="space-y-3 section-padding">
  <div class="text-center mb-12 md:mb-16 animate-fade-in-up">
    <h2
      class="text-3xl md:text-5xl font-black text-white mb-6 tracking-tight text-shadow-lg"
    >
      Choose Your Plan
    </h2>
    <div
      class="w-24 h-1 bg-gradient-to-r from-red-600 to-red-500 mx-auto mb-6 shadow-glow"
    ></div>
    <p
      class="text-lg md:text-xl text-gray-300 max-w-2xl mx-auto leading-relaxed font-light"
    >
      Flexible membership options to fit your fitness journey.
    </p>
  </div>

  <div class="grid grid-cols-1 md:grid-cols-3 gap-8">
    {#each plans as plan}
      <div class="relative">
        {#if plan.popular}
          <div
            class="absolute -top-1.5 left-1/2 transform -translate-x-1/2 z-10"
          >
            <span
              class="bg-gradient-to-r from-red-600 to-red-800 text-white text-[9px] font-semibold px-1.5 py-0.5 rounded-full shadow-sm"
            >
              MOST POPULAR
            </span>
          </div>
        {/if}

        <div
          class="h-full bg-gradient-to-br from-gray-800 to-gray-900 rounded-xl border border-gray-700 hover:border-red-600 transition-all duration-300 shadow-md hover:shadow-xl overflow-hidden flex flex-col"
        >
          <div class="p-6">
            <div class="flex items-center justify-between mb-4">
              <h3 class="text-xl font-bold text-white">{plan.name}</h3>
              {#if plan.popular}
                <div
                  class="w-2 h-2 rounded-full bg-red-500 animate-pulse"
                ></div>
              {/if}
            </div>

            <div class="mb-6">
              <p class="text-3xl font-black text-white mb-1">
                ${plan.price}<span class="text-sm font-normal text-gray-400"
                  >/{plan.period}</span
                >
              </p>
              {#if plan.id === "quarterly"}
                <p class="text-green-400 text-sm font-medium">
                  Save 12% vs monthly
                </p>
              {/if}
              {#if plan.id === "yearly"}
                <p class="text-green-400 text-sm font-medium">
                  Save 32% vs monthly
                </p>
              {/if}
            </div>

            <ul class="space-y-3 mb-6">
              {#each plan.features as feature}
                <li class="flex items-start">
                  <svg
                    class="h-5 w-5 text-green-500 mr-3 mt-0.5 flex-shrink-0"
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
                  <span class="text-gray-300 text-sm leading-relaxed"
                    >{feature}</span
                  >
                </li>
              {/each}
            </ul>
          </div>

          <div class="mt-auto p-6 pt-0">
            <button
              on:click={() => handleSubscribe(plan)}
              class="w-full py-4 px-6 rounded-xl font-bold text-lg transition-all duration-200 {activePlan ===
              plan.id
                ? 'bg-gradient-to-r from-gray-700 to-gray-800 text-gray-400 border border-gray-600 cursor-not-allowed'
                : 'bg-gradient-to-r from-red-600 to-red-700 text-white hover:from-red-700 hover:to-red-800 hover:shadow-lg hover:shadow-red-900/40 transform hover:-translate-y-1'}"
              disabled={activePlan === plan.id}
            >
              {activePlan === plan.id ? "Current Plan" : "Get Started"}
            </button>
          </div>
        </div>
      </div>
    {/each}
  </div>

  <div class="text-center mt-4">
    <p class="text-gray-400 text-[9px]">
      Need help? <a
        href="#contact"
        class="text-red-500 hover:text-red-400 transition-colors">Contact us</a
      >
    </p>
  </div>
</div>
