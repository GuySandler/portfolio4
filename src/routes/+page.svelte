<script>
	import Navbar from '$lib/components/navbar.svelte';
	import Home from '$lib/components/home.svelte';
</script>
<main>
	<Navbar />
	<main>
		<Home />
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