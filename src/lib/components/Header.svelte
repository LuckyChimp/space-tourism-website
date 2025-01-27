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
        --height="96px"
        --padding="0 64px 0 256px"
        --colorOfInactiveItems="var(--white)"
    />
</header>

<style>
    header {
        position: fixed;
        top: 40px;
        left: 64px;
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
        left: calc(48px + 64px);
        height: 1px;
        border-color: rgba(var(--white-rgb), 0.25);
        z-index: 1;
    }
</style>
