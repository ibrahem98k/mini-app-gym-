<script>
    import SubscriptionPlans from "../../components/SubscriptionPlans.svelte";
    import { goto } from "$app/navigation";

    function handlePlanSelect(plan) {
        goto(`/checkout?plan=${plan.id}`);
    }
</script>

<div class="min-h-screen bg-black pt-20">
    <div class="container-custom max-w-7xl mx-auto px-4 py-16">
        <SubscriptionPlans onSelectPlan={handlePlanSelect} />
    </div>
</div>
