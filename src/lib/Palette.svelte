<script>
	export let palette;

	import { createEventDispatcher } from "svelte";

	const dispatch = createEventDispatcher();
</script>

<div>
	{#each palette as color, i}
		<button
			class="p-4"
			style:background-color={`#${color}`}
			on:click={() => dispatch("colorchange", palette[i])}
		/>
	{/each}
</div>
