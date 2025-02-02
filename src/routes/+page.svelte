<script lang="ts">
	import MainHeader from '$lib/components/headers/MainHeader.svelte';
	import CrewSection from '$lib/components/sections/CrewSection.svelte';
	import DestinationSection from '$lib/components/sections/DestinationSection.svelte';
	import HomeSection from '$lib/components/sections/HomeSection.svelte';
	import type { PageServerData } from './$types';

	// Props
	let { data }: { data: PageServerData } = $props();

	// States
	let activeNavbarItemIndex = $state(0);

	// Event listeners
	// Change active navbar item when scrolling through the website
	const handleOnWindowScroll = () => {
		const sections = document.querySelectorAll('main > section') as NodeListOf<HTMLElement>;
		sections.forEach((section, index) => {
			const sectionTop = section.offsetTop;
			const sectionBottom = sectionTop + section.offsetHeight;

			if (scrollY >= sectionTop && scrollY <= sectionBottom) {
				activeNavbarItemIndex = index;
			}
		});
	};
</script>

<svelte:head>
	<title>Space tourism</title>
</svelte:head>

<MainHeader {activeNavbarItemIndex} />
<main>
	<HomeSection />
	<DestinationSection destinations={data.destinations} />
	<CrewSection crew={data.crew} />
</main>

<svelte:window onscroll={handleOnWindowScroll} />
