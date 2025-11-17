<script>
	import Navbar from '$lib/components/navbar.svelte';

	import Home from '$lib/components/home.svelte';
	import Contact from '$lib/components/contact.svelte';

	let tabIndex = $state(0);
</script>
<main>
	<Navbar bind:value={tabIndex} />
	<main>
		<!-- <h1>Current Tab: {tabIndex}</h1> -->
		{#if tabIndex == 0}
		<Home />
		{/if}
		{#if tabIndex == 3}
		<Contact />
		{/if}
	</main>
</main>
<style>
	main {
		display: flex;
		flex-direction: column;
		align-items: center;
		/* justify-content: center; */
		height: 100vh;
		width: 100vw;
	}
</style>