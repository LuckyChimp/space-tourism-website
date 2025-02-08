<script lang="ts">
    import type { Snippet } from 'svelte';

    // Local variables
    let carouselSlidesElement: HTMLDivElement;

    // Props
    let { orientation, navigation, slides, activeIndex }: { orientation: 'landscape' | 'portrait'; navigation: Snippet; slides: Snippet; activeIndex: number } =
        $props();

    $effect(() => {
        // Scroll the carousel depending on the active index
        const slideWidth = carouselSlidesElement.clientWidth;
        const slideHeight = carouselSlidesElement.clientHeight;
        const offset = activeIndex === 0 ? 0 : activeIndex * 600;
        const xScroll = { left: slideWidth * activeIndex + offset, behavior: 'smooth' as ScrollBehavior };
        const yScroll = { top: slideHeight * activeIndex + offset, behavior: 'smooth' as ScrollBehavior };

        carouselSlidesElement.scrollTo(orientation === 'landscape' ? xScroll : yScroll);
    });
</script>

<div class="carousel" class:orientation-landscape={orientation === 'landscape'} class:orientation-portrait={orientation === 'portrait'}>
    {@render navigation()}
    <div
        class="carousel-slides"
        class:orientation-landscape={orientation === 'landscape'}
        class:orientation-portrait={orientation === 'portrait'}
        bind:this={carouselSlidesElement}
    >
        {@render slides()}
    </div>
</div>

<style>
    .carousel {
        height: 100%;
        display: flex;
        position: relative;
        overflow: hidden;
    }

    .carousel.orientation-landscape {
        flex-direction: column;
        mask: linear-gradient(to left, transparent 0%, var(--white) 15% 85%, transparent 100%);
    }

    .carousel.orientation-portrait {
        flex-direction: row;
        gap: var(--800);
        mask: linear-gradient(to bottom, transparent 0%, var(--white) 15% 85%, transparent 100%);
    }

    .carousel-slides {
        display: flex;
        gap: 600px; /* WATCH OUT has to match the above factor of activeIndex for calculaton of the offset */
        overflow: hidden;
    }

    .carousel-slides.orientation-landscape {
        height: 100%;
        flex-direction: row;
    }

    .carousel-slides.orientation-portrait {
        width: 100%;
        flex-direction: column;
    }
</style>
