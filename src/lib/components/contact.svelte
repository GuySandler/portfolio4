<script>
	import { fade } from 'svelte/transition';
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
		loadItems(1, 300);
	});
</script>
<div id="contact" in:fade={{ duration: dur, delay: dur }} out:fade={{ duration: dur }}>
	{#if currentItems >= 1}
	<div class="card" style="text-align: left;background-color:#0ffd07;">
		<h2 style="font-size: 1.75rem;">Contact Me</h2>
		<p style="font-weight: normal;font-size:1.5rem;">Feel free to reach out to me at</p>
	</div>
	{/if}
</div>
<style>
	#contact {
		font-size: 2rem;
		font-weight: bold;
		text-align: center;
		width:100%;
		display: flex;
		flex-direction: column;
		align-items: center;
		margin-top: 10rem;
	}
	.card {
		margin: 2rem;
		padding: 2rem;
		width: 55%;
		border-radius: 15px;
		/* background-color: red; */
	}
</style>