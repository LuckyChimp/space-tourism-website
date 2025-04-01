<script lang="ts">
	import MainHeader from '$lib/components/headers/MainHeader.svelte';
	import CrewSection from '$lib/components/sections/CrewSection.svelte';
	import DestinationSection from '$lib/components/sections/DestinationSection.svelte';
	import HomeSection from '$lib/components/sections/HomeSection.svelte';
	import TechnologySection from '$lib/components/sections/TechnologySection.svelte';
	import type { PageServerData } from './$types';

	// Local variables
	const navbarSections = ['Home', 'Destination', 'Crew', 'Technology'];

	// Props
	let { data }: { data: PageServerData } = $props();

	// States
	let activeNavbarItemIndex = $state(0);

	// Event listeners
	// Change active navbar item when scrolling through the website
	const onWindowScroll = () => {
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
<svelte:window onscroll={onWindowScroll} />

<MainHeader {activeNavbarItemIndex} {navbarSections} />
<main>
	<HomeSection />
	<DestinationSection destinations={data.destinations} />
	<CrewSection crew={data.crew} />
	<TechnologySection technology={data.technology} />
</main>
