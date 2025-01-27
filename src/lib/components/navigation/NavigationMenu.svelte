<script lang="ts">
    import NavigationItem from '$lib/components/navigation/NavigationItem.svelte';
    import NavigationSlider from '$lib/components/navigation/NavigationSlider.svelte';

    let {
        sections,
        activeIndex,
        onItemClick,
        usePrefixes,
        displayBackground,
    }: {
        sections: string[];
        activeIndex: number;
        onItemClick: (index: number) => void;
        usePrefixes: boolean;
        displayBackground: boolean;
    } = $props();

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
    <NavigationSlider {activeIndex} {itemWidths} />
</nav>

<style>
    nav {
        height: var(--height, 96px);
        position: relative;
        display: flex;
        align-items: center;
        flex-direction: row;
        gap: 48px;
        padding: var(--padding, 0 64px 0 256px);
    }

    nav.display-background {
        background: rgba(var(--white-rgb), 0.05);
        box-shadow: 0 4px 30px rgba(0, 0, 0, 0.1);
        backdrop-filter: blur(40px);
        -webkit-backdrop-filter: blur(40px);
    }
</style>
