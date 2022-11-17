<script>
	import { onMount } from "svelte";

	const PIXEL_SIZE = 20;
	const PALETTE = [
		"000000",
		"1D2B53",
		"7E2553",
		"008751",
		"AB5236",
		"5F574F",
		"C2C3C7",
		"FFF1E8",
		"FF004D",
		"FFA300",
		"FFEC27",
		"00E436",
		"29ADFF",
		"83769C",
		"FF77A8",
		"FFCCAA",
	];

	let layer = [];
	let dimension = { width: 16, height: 16 };
	let selectedColor = PALETTE[7];
	let canvas;

	onMount(() => {
		const ctx = canvas.getContext("2d");

		for (let i = 0; i < dimension.height; i++) {
			for (let j = 0; j < dimension.width; j++) {}
		}
	});
</script>

<div>
	<h1>Pixi Draw</h1>
</div>

<div>
	<canvas
		bind:this={canvas}
		width={dimension.width * PIXEL_SIZE}
		height={dimension.height * PIXEL_SIZE}
	/>
</div>

<div />
