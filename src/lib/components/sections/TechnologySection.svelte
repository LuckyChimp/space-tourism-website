<script lang="ts">
    import Carousel from '$lib/components/carousel/Carousel.svelte';
    import TechnologySlide from '$lib/components/carousel/slides/TechnologySlide.svelte';
    import SectionHeader from '$lib/components/headers/SectionHeader.svelte';
    import Pagination from '$lib/components/Pagination.svelte';
    import type { PageServerData } from '../../../routes/$types';

    // Other Functions
    const getDeviceType = (innerWindowWidth: number) => {
        if (innerWindowWidth > 425 && innerWindowWidth <= 768) {
            return 'tablet';
        } else if (innerWindowWidth <= 425) {
            return 'mobile';
        } else {
            return 'desktop';
        }
    };

    // Props
    let { technology }: { technology: PageServerData['technology'] } = $props();

    // States
    let activeTechnologyIndex = $state(0);
    let innerWindowWidth = $state(0);
    let contentOrientation: 'landscape' | 'portrait' = $derived(innerWindowWidth <= 1336 ? 'landscape' : 'portrait');
    let deviceType: 'desktop' | 'tablet' | 'mobile' = $derived(getDeviceType(innerWindowWidth));
    let slideImageHeight = $state(0);

    // Local variables
    const paginationTopOffsets = {
        desktop: 96,
        tablet: 64,
        mobile: 48,
    };

    // Event listeners
    const onPaginationItemClick = (index: number) => {
        if (index !== activeTechnologyIndex) {
            activeTechnologyIndex = index;
        }
    };
</script>

<svelte:window bind:innerWidth={innerWindowWidth} />

<section id="technology">
    <SectionHeader sectionNumber="03" heading="Space launch 101" --padding-left={contentOrientation === 'landscape' ? 'var(--section-padding-left)' : '0'} />
    <Carousel orientation={contentOrientation} activeIndex={activeTechnologyIndex} showEdgeFade={contentOrientation === 'landscape' ? false : true}>
        {#snippet navigation()}
            <!-- WATCH OUT: back added value of top property must always match half of the flex gap in the split layout so that pagination container can be vertically centered -->
            <div class="pagination-container" style={`top: ${slideImageHeight + paginationTopOffsets[deviceType]}px;`}>
                <Pagination
                    type="largeWithNumbers"
                    orientation={contentOrientation}
                    activeIndex={activeTechnologyIndex}
                    length={technology.length}
                    onItemClick={onPaginationItemClick}
                />
            </div>
        {/snippet}
        {#snippet slides()}
            {#each technology as technology}
                <TechnologySlide
                    name={technology.name}
                    description={technology.description}
                    image={contentOrientation === 'landscape' ? technology.images.landscape : technology.images.portrait}
                    orientation={contentOrientation}
                    bind:imageHeight={slideImageHeight}
                />
            {/each}
        {/snippet}
    </Carousel>
</section>

<style>
    #technology {
        min-height: 100vh;
        display: flex;
        flex-direction: column;
        justify-content: space-between;
        padding-top: var(--section-padding-top);
        padding-bottom: var(--section-padding-bottom);
        padding-left: var(--section-padding-left);
        background-image: url('/images/technology/background-technology-desktop.jpg');
        background-size: cover;
        background-repeat: no-repeat;
    }

    .pagination-container {
        display: flex;
        z-index: 1;
    }

    @media screen and (max-width: 1336px) {
        #technology {
            padding-left: 0;
            gap: var(--800);
            background-image: url('/images/technology/background-technology-tablet.jpg');
        }

        .pagination-container {
            position: absolute;
            left: 50%;
            transform: translate(-50%, -50%);
            transition: all 300ms ease-out;
        }
    }

    @media screen and (max-width: 768px) {
        #technology {
            padding-top: calc(var(--300) + var(--600) + var(--300) + var(--300));
            padding-bottom: var(--300);
        }
    }

    @media screen and (max-width: 425px) {
        #technology {
            background-image: url('/images/technology/background-technology-mobile.jpg');
        }
    }
</style>
