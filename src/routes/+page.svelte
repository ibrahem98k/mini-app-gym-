<script>
	import { onMount } from "svelte";
	import { fade } from "svelte/transition";
	import { goto } from "$app/navigation";
	import Hero from "../components/Hero.svelte";
	import SubscriptionPlans from "../components/SubscriptionPlans.svelte";
	import About from "../components/About.svelte";
	import GymMap from "../components/GymMap.svelte";
	import WelcomePage from "../components/WelcomePage.svelte";
	import { isWelcomeActive } from "$lib/appStore";

	let mounted = false;

	onMount(() => {
		mounted = true;
		const hasEntered = sessionStorage.getItem("hasEntered");
		if (hasEntered) {
			isWelcomeActive.set(false);
		}
	});

	function handleEnter() {
		isWelcomeActive.set(false);
		sessionStorage.setItem("hasEntered", "true");
	}

	function handlePlanSelect(plan) {
		goto(`/checkout?plan=${plan.id}`);
	}
</script>

{#if mounted}
	{#if $isWelcomeActive}
		<div out:fade={{ duration: 400 }}>
			<WelcomePage onContinue={handleEnter} />
		</div>
	{:else}
		<main in:fade={{ duration: 400 }}>
			<Hero />
			<SubscriptionPlans onSelectPlan={handlePlanSelect} />
			<About />
			<GymMap />
		</main>
	{/if}
{/if}
