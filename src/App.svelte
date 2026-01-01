<script>
  import { onMount } from "svelte";
  import WelcomePage from "./components/WelcomePage.svelte";
  import Header from "./components/Header.svelte";
  import Hero from "./components/Hero.svelte";
  import SubscriptionStatus from "./components/SubscriptionStatus.svelte";
  import SubscriptionPlans from "./components/SubscriptionPlans.svelte";
  import GymMap from "./components/GymMap.svelte";
  import About from "./components/About.svelte";
  import Footer from "./components/Footer.svelte";
  import PlanDetails from "./components/PlanDetails.svelte";

  let showWelcome = true;
  let selectedPlan = null;
  let subscription = {
    active: false,
    plan: null,
    startDate: null,
    endDate: null,
    daysLeft: 0,
  };

  onMount(() => {
    // Load subscription from localStorage
    const stored = localStorage.getItem("gymSubscription");
    if (stored) {
      subscription = JSON.parse(stored);
    }
  });

  function handlePlanSelection(plan) {
    selectedPlan = plan;
  }

  function handlePayment(plan) {
    // If we're in a super-app environment (my exists)
    if (typeof my !== "undefined" && my.tradePay) {
      // Simulate/Initiate payment using my.tradePay
      my.tradePay({
        // In a real scenario, tradeNO would come from your backend after creating an order
        tradeNO: '2017111521001104105336677922', 
        success: (res) => {
          // Check for success status (9000 is success in many Alipay-based systems)
          if (res.resultCode === "9000" || res.resultCode === "success") {
            completeSubscription(plan);
          } else {
            console.error("Payment failed or cancelled:", res);
            if (my.alert) {
              my.alert({
                title: 'Payment Status',
                content: 'Payment was not completed. Please try again.',
              });
            }
          }
        },
        fail: (res) => {
          console.error("Payment API error:", res);
        }
      });
    } else {
      // Fallback/Demo flow for non-super-app environment
      console.log("Not in super-app environment, simulating payment success...");
      completeSubscription(plan);
    }
  }

  function completeSubscription(plan) {
    const endDate = new Date();
    endDate.setDate(
      endDate.getDate() +
        (plan.id === "monthly" ? 30 : plan.id === "quarterly" ? 90 : 365),
    );

    subscription = {
      active: true,
      plan,
      startDate: new Date(),
      endDate,
      daysLeft: plan.id === "monthly" ? 30 : plan.id === "quarterly" ? 90 : 365,
    };

    localStorage.setItem("gymSubscription", JSON.stringify(subscription));

    // Notify user of success if in super-app
    if (typeof my !== "undefined" && my.alert) {
      my.alert({
        title: 'Subscription Active',
        content: `You are now subscribed to the ${plan.name} plan!`,
      });
    }

    // Reset selection and scroll to top
    selectedPlan = null;
    window.scrollTo({ top: 0, behavior: "smooth" });
  }

  function handleContinue() {
    showWelcome = false;
  }
</script>

{#if showWelcome}
  <WelcomePage onContinue={handleContinue} />
{:else if selectedPlan}
  <PlanDetails
    plan={selectedPlan}
    onBack={() => (selectedPlan = null)}
    onPay={handlePayment}
  />
{:else}
  <main class="min-h-screen bg-black">
    <Header />

    <div class="container-custom max-w-7xl mx-auto px-4 py-16">
      <Hero />

      <div class="grid grid-cols-1 lg:grid-cols-3 gap-12 mt-20">
        <!-- Subscription Status -->
        <div class="lg:col-span-2 space-y-12">
          <SubscriptionStatus {subscription} />
          <div id="contact">
            <GymMap />
          </div>
        </div>

        <!-- Subscription Plans -->
        <div id="plans">
          <SubscriptionPlans
            activePlan={subscription.plan?.id}
            onSelectPlan={handlePlanSelection}
          />
        </div>
      </div>

      <About class="mt-24" />
    </div>

    <Footer />
  </main>
{/if}
