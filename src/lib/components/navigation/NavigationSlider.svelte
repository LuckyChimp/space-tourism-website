<script lang="ts">
    let {
        activeIndex,
        orientation,
        itemDimensions,
    }: { activeIndex: number; orientation: 'horizontal' | 'vertical'; itemDimensions: { width: number; height: number }[] } = $props();

    // Local variables
    let slider: HTMLDivElement;

    $effect(() => {
        updateSlider();
    });

    // Move slider according to the current section
    const updateSlider = () => {
        if (activeIndex === -1) return;

        if (orientation === 'horizontal') {
            slider.style.height = '3px';
            slider.style.width = `${itemDimensions[activeIndex].width}px`;
            slider.style.transform = `translateX(${calcXOffsetOfSlider(activeIndex)}px)`;
        } else if (orientation === 'vertical') {
            slider.style.width = '3px';
            slider.style.height = `${itemDimensions[activeIndex].height}px`;
            slider.style.transform = `translateY(${calcYOffsetOfSlider(activeIndex)}px)`;
        }
    };

    // Calculate gap between navigation items
    const calcNavigationItemGap = () => {
        const navigationItems = slider.parentElement?.getElementsByClassName('navigation-items')[0].children!;

        if (orientation === 'horizontal') {
            return navigationItems[1].getBoundingClientRect().left - navigationItems[0].getBoundingClientRect().right;
        } else {
            return navigationItems[1].getBoundingClientRect().top - navigationItems[0].getBoundingClientRect().bottom;
        }
    };

    // Calculate the x offset of the slider
    const calcXOffsetOfSlider = (index: number) => {
        const gap = calcNavigationItemGap(); // Gap between nav items
        return itemDimensions.slice(0, index).reduce((offset, dimensions) => offset + dimensions.width, index * gap);
    };

    // Calculate the y offset of the slider
    const calcYOffsetOfSlider = (index: number) => {
        const gap = calcNavigationItemGap(); // Gap between nav items
        return itemDimensions.slice(0, index).reduce((offset, dimensions) => offset + dimensions.height, index * gap);
    };
</script>

<div class="slider" class:vertical={orientation === 'vertical'} bind:this={slider}></div>

<style>
    :global(nav:has(.navbar-item.active:hover)) .slider {
        background-color: rgba(var(--white-rgb), 0.6);
    }

    :global(nav) .slider {
        height: 3px;
        position: absolute;
        bottom: 0;
        background-color: var(--white);
        transition: all 300ms ease-out;
    }

    @media screen and (max-width: 768px) {
        :global(nav) .slider.vertical {
            width: 3px;
            top: calc(var(--1200) + var(--200));
            right: 0;
        }
    }
</style>
