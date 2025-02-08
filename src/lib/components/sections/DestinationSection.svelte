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
                    usePrefixes={false}
                    displayBackground={false}
                    onItemClick={onTabBarItemClick}
                    itemGap={32}
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
        height: 100vh;
        display: flex;
        flex-flow: column nowrap;
        padding-top: var(--section-padding-top);
        padding-bottom: var(--section-padding-bottom);
        background-image: url('images/destination/background-destination-desktop.jpg');
        background-size: cover;
        background-repeat: no-repeat;
    }

    .tab-bar-container {
        position: absolute;
        top: var(--800);
        left: 50%;
    }
</style>
