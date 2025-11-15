<script>
	import Splash from '../Splash.svelte';
	import { post } from '../utils';
	import FobImg from '$lib/images/Fob.webp';
	import Fob from '../Fob.svelte';

	let splash = $state(true);
	post(() => (splash = false), 2000);

	const R = 80;
	const N = 16;
	const r = R * Math.sin(Math.PI / N);
	const center = { cx: 500, cy: 200 };
</script>

<div class="app">
	{#each [0, 1, 2, 3] as _, j}
		{#each Array(N) as _, i}
			{@const cx = center.cx + R * Math.cos((2 * Math.PI * i) / N)}
			{@const cy = center.cy + 2 * R * j + R * Math.sin((2 * Math.PI * i) / N)}
			{#if j % 2 ? cx <= center.cx : cx >= center.cx}
				<Fob fob={{ cx, cy, radius: r }} src={FobImg} />
			{/if}
		{/each}
	{/each}
	{#if splash}
		<Splash />
	{/if}
</div>

<style>
	.app {
		display: grid;
		height: 100dvh;
		-webkit-user-select: none;
		user-select: none;
		overflow: hidden;
		touch-action: manipulation;
		outline: none !important;
		/* background-image: url('$lib/images/Sky.jpg'); */
		/* background-position-x: center; */
		/* background-position-y: center; */
		box-sizing: border-box;
		/* border: 1px solid yellow; */
	}
</style>
