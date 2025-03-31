<script lang="ts">
    import { goto } from '$app/navigation';
    import Logo from '$lib/components/Logo.svelte';
    import Navbar from '$lib/components/navigation/NavigationMenu.svelte';

    // Props
    let { activeNavbarItemIndex, navbarSections }: { activeNavbarItemIndex: number; navbarSections: string[] } = $props();

    // Event listeners
    const onNavbarItemClick = (index: number) => goto(`#${navbarSections[index].toLowerCase()}`);
</script>

<header>
    <Logo />
    <hr />
    <Navbar
        sections={navbarSections}
        activeIndex={activeNavbarItemIndex}
        usePrefixes
        displayBackground
        onItemClick={onNavbarItemClick}
        itemGap={48}
        --itemGap="var(--600)"
        --height="var(--1200)"
        --padding="0 var(--800) 0 var(--3200)"
        --colorOfInactiveItems="var(--white)"
    />
</header>

<style>
    header {
        position: fixed;
        top: var(--500);
        left: var(--800);
        right: 0;
        display: flex;
        flex-direction: row;
        align-items: center;
        justify-content: space-between;
        z-index: 1;
    }

    hr {
        width: 50%;
        position: absolute;
        left: calc(var(--600) + var(--800));
        z-index: 1;
    }
</style>
