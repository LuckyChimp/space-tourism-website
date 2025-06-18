<script lang="ts">
    import Carousel from '$lib/components/carousel/Carousel.svelte';
    import DestinationCarouselSlide from '$lib/components/carousel/slides/DestinationCarouselSlide.svelte';
    import SectionHeader from '$lib/components/headers/SectionHeader.svelte';
    import TabBar from '$lib/components/navigation/NavigationMenu.svelte';
    import type { PageServerData } from '../../../routes/$types';

    // Props
    let { destinations }: { destinations: PageServerData['destinations'] } = $props();

    // Local variables
    const tabBarSections = destinations.map((destination) => destination.name);

    // States
    let activeDestinationIndex = $state(0);

    // Event listeners
    const onTabBarItemClick = (index: number) => {
        if (index !== activeDestinationIndex) {
            activeDestinationIndex = index;
        }
    };
</script>

<section id="destination">
    <SectionHeader sectionNumber="01" heading="Pick your destination" />
    <Carousel orientation="landscape" activeIndex={activeDestinationIndex}>
        {#snippet navigation()}
            <div class="tab-bar-container">
                <TabBar
                    sections={tabBarSections}
                    activeIndex={activeDestinationIndex}
                    context="carousel"
                    onItemClick={onTabBarItemClick}
                    --itemGap="var(--400)"
                    --height="var(--400)"
                    --padding="0"
                    --colorOfInactiveItems="var(--light-blue)"
                />
            </div>
        {/snippet}
        {#snippet slides()}
            {#each destinations as destination}
                <DestinationCarouselSlide
                    name={destination.name}
                    description={destination.description}
                    distance={destination.distance}
                    travelTime={destination.travel}
                    image={destination.images.png}
                />
            {/each}
        {/snippet}
    </Carousel>
</section>

<style>
    #destination {
        min-height: 100vh;
        display: flex;
        flex-flow: column nowrap;
        justify-content: space-between;
        gap: var(--300);
        padding-top: var(--section-padding-top);
        padding-bottom: var(--section-padding-bottom);
        background-image: url('images/destination/background-destination-desktop.jpg');
        background-size: cover;
        background-repeat: no-repeat;
    }

    .tab-bar-container {
        position: absolute;
        left: calc(50% + var(--300));
        z-index: 1;
    }

    @media screen and (max-width: 1276px) {
        #destination {
            gap: var(--800);
            background-image: url('images/destination/background-destination-tablet.jpg');
        }

        .tab-bar-container {
            top: calc(445px + var(--1000));
            transform: translateX(-50%);
            left: 50%;
        }
    }

    @media screen and (max-width: 900px) {
        #destination {
            padding-top: calc(var(--300) + var(--600) + var(--300) + var(--500));
            padding-bottom: var(--500);
        }
    }

    @media screen and (max-width: 768px) {
        #destination {
            gap: var(--600);
            padding-top: calc(var(--300) + var(--600) + var(--300) + var(--300));
            padding-bottom: var(--300);
        }

        .tab-bar-container {
            top: calc(300px + var(--1000));
        }
    }

    @media screen and (max-width: 425px) {
        #destination {
            background-image: url('images/destination/background-destination-mobile.jpg');
        }

        .tab-bar-container {
            top: calc(150px + var(--800));
        }
    }
</style>
