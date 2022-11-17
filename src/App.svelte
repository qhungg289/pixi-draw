<script>
	import TitleBar from "./lib/TitleBar.svelte";
	import Palette from "./lib/Palette.svelte";
	import CurrentColor from "./lib/CurrentColor.svelte";

	import { onMount } from "svelte";

	const PIXEL_SIZE = 40;
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
	let dimension = { width: 8, height: 8 };
	let selectedColor = PALETTE[8];
	let canvas;

	function draw() {
		const ctx = canvas.getContext("2d");

		for (let i = 0; i < dimension.height; i++) {
			for (let j = 0; j < dimension.width; j++) {
				const x = i * (canvas.width / dimension.width);
				const y = j * (canvas.height / dimension.height);

				ctx.fillStyle = layer[i][j];
				ctx.fillRect(x, y, PIXEL_SIZE, PIXEL_SIZE);
			}
		}
	}

	onMount(() => {
		layer = new Array(dimension.height);
		for (let i = 0; i < dimension.width; i++) {
			layer[i] = new Array(dimension.width);
		}

		for (let i = 0; i < dimension.height; i++) {
			for (let j = 0; j < dimension.width; j++) {
				layer[i][j] = PALETTE[0];
			}
		}

		draw();
	});

	$: console.table(layer);
</script>

<TitleBar />

<div class="flex items-center justify-center h-4/6">
	<canvas
		bind:this={canvas}
		width={dimension.width * PIXEL_SIZE}
		height={dimension.height * PIXEL_SIZE}
		on:click={(e) => {
			const rect = canvas.getBoundingClientRect();
			const scaleX = canvas.width / rect.width;
			const scaleY = canvas.height / rect.height;
			const x = Math.floor(((e.clientX - rect.left) * scaleX) / PIXEL_SIZE);
			const y = Math.floor(((e.clientY - rect.top) * scaleY) / PIXEL_SIZE);
			layer[y][x] = selectedColor;
			draw();
		}}
	/>
</div>

<div class="border-t-2">
	<CurrentColor {selectedColor} />

	<Palette
		palette={PALETTE}
		on:colorchange={(e) => (selectedColor = e.detail)}
	/>
</div>
