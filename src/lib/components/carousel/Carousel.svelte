<script lang="ts">
    // Local variables
    let carouselSlidesElement: HTMLDivElement;

    // Props
    let { navigation, slides, activeIndex }: { navigation: any; slides: any; activeIndex: number } = $props();

    $effect(() => {
        // Scroll the carousel depending on the active index
        const slideWidth = carouselSlidesElement.clientWidth;
        const offset = activeIndex === 0 ? 0 : activeIndex * 600;
        carouselSlidesElement.scrollTo({ left: slideWidth * activeIndex + offset, behavior: 'smooth' });
    });
</script>

<div class="carousel">
    {@render navigation()}
    <div class="carousel-slides" bind:this={carouselSlidesElement}>
        {@render slides()}
    </div>
</div>

<style>
    .carousel {
        height: 100%;
        display: flex;
        flex-direction: column;
        position: relative;
        overflow-x: hidden;
        mask: linear-gradient(to left, transparent 0%, var(--white) 15% 85%, transparent 100%);
    }

    .carousel .carousel-slides {
        height: 100%;
        display: flex;
        gap: 600px; /* WATCH OUT has to match the above factor of activeIndex for calculaton of the offset */
        overflow-x: hidden;
    }
</style>
