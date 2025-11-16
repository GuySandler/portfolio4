<script>
	// this is a button template component
	let { text } = $props();
</script>
<button>{text}</button>
<style>
	button {
		padding: 0.5rem 1rem;
		font-size: 1rem;
		border: none;
		border-radius: 15px;
		background-color: #007bff;
		color: white;
		cursor: pointer;
	}
	button:hover {
		background-color: #0056b3;
	}
</style>