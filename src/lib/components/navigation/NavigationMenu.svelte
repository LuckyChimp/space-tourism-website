<script lang="ts">
    import NavigationItem from '$lib/components/navigation/NavigationItem.svelte';
    import NavigationSlider from '$lib/components/navigation/NavigationSlider.svelte';
    import { navbar } from '$lib/globalStates.svelte';
    import { onMount } from 'svelte';
    import NavigationClose from './NavigationClose.svelte';

    // Props
    let {
        activeIndex,
        context,
        sections,
        onItemClick,
    }: {
        activeIndex: number;
        context: 'website' | 'carousel';
        sections: string[];
        onItemClick: (index: number) => void;
    } = $props();

    // States
    let orientation: 'horizontal' | 'vertical' = $state('horizontal');
    let itemDimensions: { width: number; height: number }[] = $state(Array(sections.length).fill({ width: 0, height: 0 }));

    onMount(() => {
        determineOrientation();
    });

    // Event listeners
    const onWindowResize = () => determineOrientation();

    // Other functions
    const determineOrientation = () => {
        // WATCH OUT value must be equal to the value of max-width further down in the CSS styles
        if (window.innerWidth <= 768) {
            orientation = 'vertical';
        } else {
            orientation = 'horizontal';
        }
    };
</script>

<svelte:window onresize={onWindowResize} />

<nav
    class:orientation-vertical={orientation === 'vertical' && context === 'website'}
    class:is-open={navbar.isOpen}
    class:display-background={context === 'website'}
>
    <NavigationClose />
    <div class="navigation-items">
        {#each sections as section, index}
            <NavigationItem
                {index}
                prefix={context === 'website' ? index.toLocaleString(undefined, { minimumIntegerDigits: 2 }) : null}
                active={activeIndex === index}
                onClick={onItemClick}
                bind:dimensions={itemDimensions[index]}
            >
                {section}
            </NavigationItem>
        {/each}
    </div>
    <NavigationSlider {activeIndex} {orientation} {itemDimensions} />
</nav>

<style>
    nav {
        height: var(--height, var(--1200));
        position: relative;
        padding: var(--padding, 0 var(--800) 0 var(--3200));
        z-index: 1;
    }

    nav.orientation-vertical {
        transform: translateX(100%);
        transition: all 200ms ease-out;
    }

    nav.orientation-vertical.is-open {
        transform: translateX(0);
    }

    nav.display-background {
        background: rgba(var(--white-rgb), 0.05);
        box-shadow: 0 var(--50) var(--400) rgba(0, 0, 0, 0.1);
        backdrop-filter: blur(var(--500));
        -webkit-backdrop-filter: blur(var(--500));
    }

    @media screen and (max-width: 1029px) {
        nav {
            padding-left: var(--1600);
        }
    }

    @media screen and (max-width: 901px) {
        nav {
            padding-left: var(--1200);
        }
    }

    @media screen and (max-width: 869px) {
        nav {
            padding-left: var(--1200);
            padding-right: var(--500);
        }
    }

    @media screen and (max-width: 797px) {
        nav {
            padding-left: var(--800);
            padding-right: var(--500);
        }
    }

    .navigation-items {
        height: 100%;
        display: flex;
        align-items: center;
        flex-direction: row;
        gap: var(--itemGap, var(--600));
    }

    @media screen and (max-width: 768px) {
        nav {
            position: fixed;
            top: 0;
            bottom: 0;
            right: 0;
            height: 100vh;
            padding: var(--400);
        }

        .navigation-items {
            margin-top: var(--1000);
            flex-direction: column;
            align-items: initial;
            gap: var(--400);
        }
    }
</style>
