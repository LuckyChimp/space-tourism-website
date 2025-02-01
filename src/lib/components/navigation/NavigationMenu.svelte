<script lang="ts">
    import NavigationItem from '$lib/components/navigation/NavigationItem.svelte';
    import NavigationSlider from '$lib/components/navigation/NavigationSlider.svelte';

    // Props
    let {
        sections,
        activeIndex,
        onItemClick,
        usePrefixes,
        displayBackground,
        itemGap,
    }: {
        sections: string[];
        activeIndex: number;
        onItemClick: (index: number) => void;
        usePrefixes: boolean;
        displayBackground: boolean;
        itemGap: number;
    } = $props();

    // States
    let itemWidths = $state(Array(sections.length).fill(0));
</script>

<nav class:display-background={displayBackground}>
    {#each sections as section, index}
        <NavigationItem
            {index}
            prefix={usePrefixes ? index.toLocaleString(undefined, { minimumIntegerDigits: 2 }) : null}
            active={activeIndex === index}
            onClick={onItemClick}
            bind:width={itemWidths[index]}
        >
            {section}
        </NavigationItem>
    {/each}
    <NavigationSlider {activeIndex} {itemWidths} {itemGap} />
</nav>

<style>
    nav {
        height: var(--height, var(--1200));
        position: relative;
        display: flex;
        align-items: center;
        flex-direction: row;
        gap: var(--itemGap, var(--600));
        padding: var(--padding, 0 var(--800) 0 var(--3200));
    }

    nav.display-background {
        background: rgba(var(--white-rgb), 0.05);
        box-shadow: 0 var(--50) var(--400) rgba(0, 0, 0, 0.1);
        backdrop-filter: blur(var(--500));
        -webkit-backdrop-filter: blur(var(--500));
    }
</style>
