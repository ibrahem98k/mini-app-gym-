<script>
  import { page } from "$app/stores";
  import { onMount } from "svelte";
  import "../app.css";
  import Header from "../components/Header.svelte";
  import Footer from "../components/Footer.svelte";
  import { isWelcomeActive } from "$lib/appStore";

  onMount(() => {
    // Ensure proper viewport settings
    document.documentElement.style.height = "100%";
    document.documentElement.style.width = "100%";
    document.documentElement.style.margin = "0";
    document.documentElement.style.padding = "0";
    document.documentElement.style.overflowX = "hidden";

    document.body.style.margin = "0";
    document.body.style.padding = "0";
    document.body.style.minHeight = "100vh";
    document.body.style.width = "100%";
    document.body.style.overflowX = "hidden";

    // Add smooth scrolling
    document.documentElement.style.scrollBehavior = "smooth";
  });
</script>

<svelte:head>
  <title>Gym Subscription Manager</title>
  <meta
    name="description"
    content="Track your gym subscription and view membership plans"
  />
  <style>
    :global(*) {
      box-sizing: border-box;
    }

    :global(html, body) {
      height: 100%;
      width: 100%;
      margin: 0;
      padding: 0;
      overflow-x: hidden;
    }

    :global(body) {
      min-height: 100vh;
    }

    .app-container {
      display: flex;
      flex-direction: column;
      min-height: 100vh;
      width: 100%;
    }

    main {
      flex: 1;
      width: 100%;
      overflow-x: hidden;
    }
  </style>
</svelte:head>

{#if !($page.url.pathname === "/" && $isWelcomeActive)}
  <Header />
{/if}

<main>
  <slot />
</main>

{#if !$page.url.pathname.startsWith("/checkout") && !($page.url.pathname === "/" && $isWelcomeActive)}
  <Footer />
{/if}
