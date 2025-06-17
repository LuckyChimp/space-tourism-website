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
    let crewMemberTextContainerOffsetHeights: number[] = $state(Array(crew.length));

    // Event listeners
    const onPaginationItemClick = (index: number) => {
        if (index !== activeCrewIndex) {
            activeCrewIndex = index;
        }
    };
</script>

<section id="crew">
    <SectionHeader sectionNumber="02" heading="Meet your crew" />
    <Carousel orientation="landscape" activeIndex={activeCrewIndex}>
        {#snippet slides()}
            {#each crew as crewMember, index}
                <CrewMemberCarouselSlide
                    role={crewMember.role}
                    name={crewMember.name}
                    bio={crewMember.bio}
                    image={crewMember.images.png}
                    isActive={index === activeCrewIndex}
                    bind:textContainerOffsetHeight={crewMemberTextContainerOffsetHeights[index]}
                />
            {/each}
        {/snippet}
        {#snippet navigation()}
            <!-- WATCH OUT: back added value of top property must always match half of the flex gap in the split layout so that pagination container can be vertically centered -->
            <div
                class="pagination-container"
                style={`top: ${crewMemberTextContainerOffsetHeights[activeCrewIndex] + 64}px; left: 50%; transform: translate(-50%, -50%);`}
            >
                <Pagination type="small" activeIndex={activeCrewIndex} length={crew.length} onItemClick={onPaginationItemClick} />
            </div>
        {/snippet}
    </Carousel>
</section>

<style>
    #crew {
        min-height: 100vh;
        display: flex;
        flex-direction: column;
        padding-top: var(--section-padding-top);
        padding-bottom: var(--section-padding-bottom);
        background-image: url('images/crew/background-crew-desktop.jpg');
        background-position: 0 50%;
        background-size: cover;
        background-repeat: no-repeat;
    }

    .pagination-container {
        position: absolute;
        padding-left: var(--section-padding-left);
        padding-right: var(--section-padding-right);
        z-index: 1;
        transition: all 300ms ease-out;
    }

    @media screen and (max-width: 768px) {
        #crew {
            gap: var(--600);
            padding-top: calc(var(--300) + var(--600) + var(--300) + var(--300));
            padding-bottom: var(--300);
        }
    }

    @media screen and (max-width: 425px) {
        #crew {
            background-image: url('images/crew/background-crew-mobile.jpg');
        }
    }

    /* Slide specific styles */
    /* -- 1st slide */
    @media screen and (max-width: 1497px) {
        #crew:global(:has(.split-layout:nth-child(1).active)) {
            gap: var(--800);
            background-image: url('images/crew/background-crew-tablet.jpg');
        }
    }

    @media screen and (min-width: 1498px) {
        :global(#crew:has(.split-layout:nth-child(1).active) .pagination-container) {
            bottom: 0;
            left: 0 !important;
            top: initial !important;
            transform: initial !important;
        }
    }

    /* -- 2nd slide */
    @media screen and (max-width: 1416px) {
        #crew:global(:has(.split-layout:nth-child(2).active)) {
            gap: var(--800);
            background-image: url('images/crew/background-crew-tablet.jpg');
        }
    }

    @media screen and (min-width: 1417px) {
        :global(#crew:has(.split-layout:nth-child(2).active) .pagination-container) {
            bottom: 0;
            left: 0 !important;
            top: initial !important;
            transform: initial !important;
        }
    }

    /* -- 3rd slide */
    @media screen and (max-width: 1532px) {
        #crew:global(:has(.split-layout:nth-child(3).active)) {
            gap: var(--800);
            background-image: url('images/crew/background-crew-tablet.jpg');
        }
    }

    @media screen and (min-width: 1533px) {
        :global(#crew:has(.split-layout:nth-child(3).active) .pagination-container) {
            bottom: 0;
            left: 0 !important;
            top: initial !important;
            transform: initial !important;
        }
    }

    /* -- 4th slide */
    @media screen and (max-width: 1558px) {
        #crew:global(:has(.split-layout:nth-child(4).active)) {
            gap: var(--800);
            background-image: url('images/crew/background-crew-tablet.jpg');
        }
    }

    @media screen and (min-width: 1559px) {
        :global(#crew:has(.split-layout:nth-child(4).active) .pagination-container) {
            bottom: 0;
            left: 0 !important;
            top: initial !important;
            transform: initial !important;
        }
    }
</style>
