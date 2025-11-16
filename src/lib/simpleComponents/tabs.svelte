<script lang="ts">
	let { tabs, value = $bindable(0) } = $props();

	let tabsContainer;
	let tabElements = [];
	let selectorPosition = $state({ left: 0, width: 0 });
	
	function selectTab(index) {
		value = index;
	}
	
	function updateSelectorPosition() {
		if (!tabsContainer || !tabElements[value]) return;

		const containerRect = tabsContainer.getBoundingClientRect();
		const tabRect = tabElements[value].getBoundingClientRect();
		
		selectorPosition = {
			left: tabRect.left - containerRect.left,
			width: tabRect.width
		};
	}
	
	$effect(() => {
		value;
		updateSelectorPosition();
	});
</script>
<div id="tabs" bind:this={tabsContainer}>
	{#each tabs as tab, i}
		<div 
			class="tab"
			class:active={i === value}
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