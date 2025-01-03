<script lang="ts">
	import { onMount } from 'svelte';
	import Navbar from '$lib/components/Navbar.svelte';
	import '../app.css';
	
	onMount(() => {
	  const link = document.createElement('link');
	  link.href = 'https://fonts.googleapis.com/css2?family=Syne+Mono&display=swap';
	  link.rel = 'stylesheet';
	  document.head.appendChild(link);
	});
  </script>
  
  <svelte:head>
	<title>Elie - Fashion Explorer</title>
	<meta name="description" content="Fashion explorer merging DIY with blockchain technology" />
  </svelte:head>
  
  <div class="layout">
	<Navbar />
	<main>
	  <slot />
	</main>
  </div>
  
  <style>
	.layout {
	  min-height: 100vh;
	  /* background-color: var(--color-primary); */
	  /* color: white; */
	}
  
	main {
	  padding-top: 0;
	}
  
	:global(html) {
	  scroll-behavior: smooth;
	}
  </style>