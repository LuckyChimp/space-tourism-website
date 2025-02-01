<script lang="ts">
    import Carousel from '$lib/components/carousel/Carousel.svelte';
    import DestinationCarouselSlide from '$lib/components/carousel/slides/DestinationCarouselSlide.svelte';
    import SectionHeader from '$lib/components/headers/SectionHeader.svelte';
    import TabBar from '$lib/components/navigation/NavigationMenu.svelte';
    import type { PageServerData } from '../../../routes/$types';

    // Props
    let { data }: { data: PageServerData['destinations'] } = $props();

    // Local variables
    const tabBarSections = data.map((destination) => destination.name);
    const planetImageURLs = [
        '/images/destination/image-moon.png',
        '/images/destination/image-mars.png',
        '/images/destination/image-europa.png',
        '/images/destination/image-titan.png',
    ];

    // States
    let activeDestinationIndex = $state(0);
    let planetImageFades = $state(false);
    let planetImageURL = $state(planetImageURLs[0]);

    // Event listeners
    const onTabBarItemClick = (index: number) => {
        if (index !== activeDestinationIndex) {
            activeDestinationIndex = index;

            // Set new planet image
            planetImageFades = true;
            setTimeout(() => {
                planetImageURL = planetImageURLs[index];
                planetImageFades = false;
            }, 300);
        }
    };
</script>

<section id="destination">
    <SectionHeader sectionNumber="01" heading="Pick your destination" />
    <div class="destination-content-container">
        <img src={planetImageURL} alt="moon" class:fade={planetImageFades} />
        <Carousel activeIndex={activeDestinationIndex}>
            {#snippet navigation()}
                <TabBar
                    sections={tabBarSections}
                    activeIndex={activeDestinationIndex}
                    usePrefixes={false}
                    displayBackground={false}
                    onItemClick={onTabBarItemClick}
                    itemGap={32}
                    --itemGap="var(--400)"
                    --height="var(--400)"
                    --padding="0"
                    --colorOfInactiveItems="var(--light-blue)"
                />
            {/snippet}
            {#snippet slides()}
                {#each data as destination, index}
                    <DestinationCarouselSlide
                        name={destination.name}
                        description={destination.description}
                        distance={destination.distance}
                        travelTime={destination.travel}
                        active={activeDestinationIndex === index}
                    />
                {/each}
            {/snippet}
        </Carousel>
    </div>
</section>

<style>
    #destination {
        height: 100vh;
        display: flex;
        flex-flow: column nowrap;
        padding: calc(var(--500) + var(--1200) + var(--600)) calc(var(--800) + var(--600) + var(--800)) var(--600) calc(var(--800) + var(--600) + var(--800));
        background-image: url('images/destination/background-destination-desktop.jpg');
        background-size: cover;
        background-repeat: no-repeat;
    }

    .destination-content-container {
        height: 100%;
        display: flex;
        align-items: center;
        justify-content: space-between;
        gap: var(--1000);
    }

    .destination-content-container > img {
        opacity: 1;
        transition: opacity 300ms ease-in-out; /* WATCH OUT duration has to match the above timeout while fading in onTabBarItemClick() */
    }

    .destination-content-container > img.fade {
        opacity: 0;
    }
</style>
