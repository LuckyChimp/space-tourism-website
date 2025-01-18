<script lang="ts">
	import HomeSection from '$lib/components/sections/HomeSection.svelte';
	import type { PageServerData } from './$types';

	let { data }: { data: PageServerData } = $props();
</script>

<main>
	<HomeSection />
</main>

<style>
	:global(body) {
		width: 100%;
		min-height: 100vh;
		background-image: url('images/home/background-home-desktop.jpg');
		background-size: 100% auto;
		background-repeat: no-repeat;
		background-position: 50% 0%;
	}
</style>
