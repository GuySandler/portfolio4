<script>
	import { fly } from 'svelte/transition';
	import { onMount } from 'svelte';
	let currentItems = $state(0);
	function loadItems(max, ms) {
		let interval = setInterval(() => {
			if (currentItems < max) {
				currentItems += 1;
			}
		}, ms);
		setTimeout(() => clearInterval(interval), ms * max);
	}
	let dur = 700;
	let yOffset = -20;

	onMount(() => {
		loadItems(2, 300);
	});
</script>
<div id="home" out:fly={{ y: yOffset, duration: dur }}>
	{#if currentItems >= 1}
	<div class="card" in:fly={{ y: yOffset, duration: dur }}>
		<h1>Hi, I'm Guy Sandler</h1>
		<h2>Developer, Maker, and Student</h2>
	</div>
	{/if}
	{#if currentItems >= 2}
	<div class="card" style="text-align: left;background-color:#0ffd07;" in:fly={{ y: yOffset, duration: dur }}>
		<h2 style="font-size: 1.75rem;">About me</h2>
		<p style="font-weight: normal;font-size:1.5rem;">I am a 16 year old student in the Bay Area. In my free time I make apps and engineer things with my 3d printer.</p>
	</div>
	{/if}
</div>
<style>
	#home {
		font-size: 2rem;
		font-weight: bold;
		text-align: center;
		width:100%;
		display: flex;
		flex-direction: column;
		align-items: center;
		margin-top: 10rem;
	}
	h1 {
		font-size: 3rem;
	}
	.card {
		margin: 2rem;
		padding: 2rem;
		width: 55%;
		border-radius: 15px;
		/* background-color: red; */
	}
</style>