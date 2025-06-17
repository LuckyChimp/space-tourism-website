<script lang="ts">
    import Carousel from '$lib/components/carousel/Carousel.svelte';
    import TechnologySlide from '$lib/components/carousel/slides/TechnologySlide.svelte';
    import SectionHeader from '$lib/components/headers/SectionHeader.svelte';
    import Pagination from '$lib/components/Pagination.svelte';
    import type { PageServerData } from '../../../routes/$types';

    // Props
    let { technology }: { technology: PageServerData['technology'] } = $props();

    // States
    let activeTechnologyIndex = $state(0);

    // Event listeners
    const onPaginationItemClick = (index: number) => {
        if (index !== activeTechnologyIndex) {
            activeTechnologyIndex = index;
        }
    };
</script>

<section id="technology">
    <SectionHeader sectionNumber="03" heading="Space launch 101" --padding-left="0" />
    <Carousel orientation="portrait" activeIndex={activeTechnologyIndex}>
        {#snippet navigation()}
            <Pagination
                type="largeWithNumbers"
                orientation={contentOrientation}
                activeIndex={activeTechnologyIndex}
                length={technology.length}
                onItemClick={onPaginationItemClick}
            />
        {/snippet}
        {#snippet slides()}
            {#each technology as technology}
                <TechnologySlide name={technology.name} description={technology.description} image={technology.images.portrait} />
            {/each}
        {/snippet}
    </Carousel>
</section>

<style>
    #technology {
        min-height: 100vh;
        display: flex;
        flex-direction: column;
        padding-top: var(--section-padding-top);
        padding-bottom: var(--section-padding-bottom);
        padding-left: var(--section-padding-left);
        background-image: url('images/technology/background-technology-desktop.jpg');
        background-size: cover;
        background-repeat: no-repeat;
    }
</style>
