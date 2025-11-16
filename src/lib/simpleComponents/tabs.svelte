<script lang="ts">
	let { tabs } = $props();
	import { quintOut } from 'svelte/easing';
	import { crossfade } from 'svelte/transition';

	const [send, receive] = crossfade({
		duration: d => Math.sqrt(d * 200),

		fallback(node, params) {
			return {
				duration: 600,
				easing: quintOut,
				css: t => `opacity: ${t}`
			};
		}
	});

	let selectedTab = $state(0);
	let tabsContainer: HTMLDivElement;
	let tabElements: HTMLDivElement[] = [];
	let selectorPosition = $state({ left: 0, width: 0 });
	
	function selectTab(index: number) {
		selectedTab = index;
	}
	
	function updateSelectorPosition() {
		if (!tabsContainer || !tabElements[selectedTab]) return;
		
		const containerRect = tabsContainer.getBoundingClientRect();
		const tabRect = tabElements[selectedTab].getBoundingClientRect();
		
		selectorPosition = {
			left: tabRect.left - containerRect.left,
			width: tabRect.width
		};
	}
	
	$effect(() => {
		selectedTab;
		updateSelectorPosition();
	});
</script>
<div id="tabs" bind:this={tabsContainer}>
	{#each tabs as tab, i}
		<div 
			class="tab"
			class:active={i === selectedTab}
			bind:this={tabElements[i]}
			onclick={() => selectTab(i)}
			onkeydown={(e) => e.key === 'Enter' && selectTab(i)}
			role="button"
			tabindex="0"
		>
			{tab.text}
		</div>
	{/each}
	<div 
		id="selector"
		style:left="{selectorPosition.left}px"
		style:width="{selectorPosition.width}px"
	></div>
</div>
<style>
	#tabs {
		display: flex;
		align-items: center;
		justify-content: space-around;
		background-color: #77cdfe;
		gap: 1rem;
		padding: .6rem 1.5rem;
		border-radius: 15px;
		position: relative;
	}
	
	.tab {
		cursor: pointer;
		user-select: none;
		transition: opacity 0.2s ease;
		z-index: 1;
		font-weight: 600;
		opacity: 0.5;
	}
	
	.tab:hover {
		opacity: 0.7;
	}
	
	.tab.active {
		opacity: 1;
	}
	
	#selector {
		height: 3px;
		background-color: #4c6afd;
		position: absolute;
		bottom: 10px;
		border-radius: 5px;
		z-index: 100;
		transition: left 0.3s cubic-bezier(0.4, 0, 0.2, 1), width 0.3s cubic-bezier(0.4, 0, 0.2, 1);
	}
</style>