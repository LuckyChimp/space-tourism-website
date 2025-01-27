<script lang="ts">
	import Header from '$lib/components/Header.svelte';
	import DestinationSection from '$lib/components/sections/DestinationSection.svelte';
	import HomeSection from '$lib/components/sections/HomeSection.svelte';
	import type { PageServerData } from './$types';

	let { data }: { data: PageServerData } = $props();
</script>

<svelte:head>
	<title>Space tourism</title>
</svelte:head>

<Header />
<main>
	<HomeSection />
	<DestinationSection data={data.destinations} />
</main>

<!-- TODO Implement scroll snap with snap points for each section -->
