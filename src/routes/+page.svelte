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
	const center = { cx: 100, cy: 0 };
</script>

<div class="app">
	<div class="axis"></div>
	{#each Array(40) as _, i}
		{@const cx = center.cx + i * 25}
		{@const angle = i * (Math.PI / 18)}
		{@const cy = center.cy + Math.cos(angle) * 100}
		<Fob fob={{ cx, cy, radius: 10 }} src={FobImg} />
	{/each}
	<!-- {#if splash}
		<Splash />
	{/if} -->
</div>

<style>
	.app {
		display: grid;
		align-content: center;
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

	.axis {
		grid-area: 1/1;
		align-self: center;
		width: 100%;
		height: 1px;
		background: #d2b48c80;
	}
</style>
