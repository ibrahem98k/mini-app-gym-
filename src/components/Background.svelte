<script>
  import { onMount } from 'svelte';
  
  onMount(() => {
    // Ensure the background covers the entire viewport
    document.documentElement.style.height = '100%';
    document.body.style.height = '100%';
    document.body.style.margin = '0';
    document.body.style.padding = '0';
    document.body.style.overflow = 'hidden';
  });
</script>

<svelte:head>
  <style>
    :global(html), :global(body), :global(#app), :global(#svelte) {
      height: 100%;
      width: 100%;
      margin: 0;
      padding: 0;
      overflow-x: hidden;
    }
    
    :global(body) {
      background: linear-gradient(-45deg, #1a1a1a, #2d1e2f, #1e2f2f, #2f1e1e);
      background-size: 400% 400%;
      animation: gradientBG 15s ease infinite;
      font-family: 'Inter', sans-serif;
      -webkit-font-smoothing: antialiased;
      -moz-osx-font-smoothing: grayscale;
    }
    
    @keyframes gradientBG {
      0% { background-position: 0% 50%; }
      50% { background-position: 100% 50%; }
      100% { background-position: 0% 50%; }
    }
    
    .content {
      position: relative;
      z-index: 1;
      min-height: 100vh;
      width: 100%;
    }
  </style>
</svelte:head>

<div class="content">
  <slot />
</div>
