<script>
	import Tabs from '$lib/simpleComponents/tabs.svelte';
	let { value = $bindable(0) } = $props();
</script>
<div id="navbar">
	<Tabs tabs={[{text:"Home"}, {text:"Projects"}, {text: "Experience"},{text:"Contact"}]} bind:value />
</div>
<style>
	#navbar {
		width: 100%;
		/* background-color:aqua; */
		height: 4rem;
		display: flex;
		align-items: center;
		justify-content: center;
	}
</style>