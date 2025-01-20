<script lang="ts">
    let { activeItemIndex, itemWidths }: { activeItemIndex: number; itemWidths: number[] } = $props();

    let slider: HTMLDivElement;

    $effect(() => {
        updateSlider();
    });

    // Move slider according to the current section
    const updateSlider = () => {
        if (activeItemIndex === -1) return;

        slider.style.width = `${itemWidths[activeItemIndex]}px`;
        slider.style.transform = `translateX(${calcXOffsetOfSlider(activeItemIndex)}px)`;
    };

    // Calculate the x offset of the slider
    const calcXOffsetOfSlider = (index: number) => {
        const gap = 48; // Gap between nav items
        return itemWidths.slice(0, index).reduce((offset, width) => offset + width, index * gap);
    };
</script>

<div class="slider" bind:this={slider}></div>

<style>
    :global(nav:has(.navbar-item.active:hover)) .slider {
        background-color: rgba(var(--white-rgb), 0.6);
    }

    :global(nav) .slider {
        height: 3px;
        position: absolute;
        bottom: 0;
        background-color: var(--white);
        transition: all ease-out 300ms;
    }
</style>
