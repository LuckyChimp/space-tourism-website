<script lang="ts">
    import Carousel from '$lib/components/carousel/Carousel.svelte';
    import CrewMemberCarouselSlide from '$lib/components/carousel/slides/CrewMemberCarouselSlide.svelte';
    import SectionHeader from '$lib/components/headers/SectionHeader.svelte';
    import Pagination from '$lib/components/Pagination.svelte';
    import type { PageServerData } from '../../../routes/$types';

    // Props
    let { crew }: { crew: PageServerData['crew'] } = $props();

    // States
    let activeCrewIndex = $state(0);

    // Event listeners
    const onPaginationItemClick = (index: number) => {
        if (index !== activeCrewIndex) {
            activeCrewIndex = index;
        }
    };
</script>

<section id="crew">
    <SectionHeader sectionNumber="02" heading="Meet your crew" />
    <Carousel activeIndex={activeCrewIndex}>
        {#snippet slides()}
            {#each crew as crewMember}
                <CrewMemberCarouselSlide role={crewMember.role} name={crewMember.name} bio={crewMember.bio} image={crewMember.images.png} />
            {/each}
        {/snippet}
        {#snippet navigation()}
            <div class="pagination-container">
                <Pagination activeIndex={activeCrewIndex} length={crew.length} onItemClick={onPaginationItemClick} --padding-bottom="var(--600)" />
            </div>
        {/snippet}
    </Carousel>
</section>

<style>
    #crew {
        height: 100vh;
        display: flex;
        flex-direction: column;
        padding: var(--section-padding-top-bottom);
        background-image: url('images/crew/background-crew-desktop.jpg');
        background-position: 0 50%;
        background-size: cover;
        background-repeat: no-repeat;
    }

    .pagination-container {
        position: absolute;
        bottom: 0;
        left: 0;
        padding: var(--section-padding-left-right);
    }
</style>
