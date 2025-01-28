<script lang="ts">
    import { goto } from '$app/navigation';
    import { page } from '$app/state';
    import Logo from '$lib/components/Logo.svelte';
    import Navbar from '$lib/components/navigation/NavigationMenu.svelte';

    // Local variables
    const navbarSections = ['Home', 'Destination', 'Crew', 'Technology'];
    const validHashes = navbarSections.map((section) => `#${section.toLowerCase()}`);

    // States
    let activeNavbarItemIndex = $state(0);

    $effect(() => {
        activeNavbarItemIndex = validHashes.indexOf(page.url.hash);
    });

    // Event listeners
    const onNavbarItemClick = (index: number) => goto(`#${navbarSections[index].toLowerCase()}`);
</script>

<header>
    <Logo />
    <hr />
    <!-- FIXME Active navbar item doesnt change when scrolling through the website -->
    <Navbar
        sections={navbarSections}
        activeIndex={activeNavbarItemIndex}
        usePrefixes
        displayBackground
        onItemClick={onNavbarItemClick}
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
        height: 1px;
        border-color: rgba(var(--white-rgb), 0.25);
        z-index: 1;
    }
</style>
