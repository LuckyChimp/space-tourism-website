<script lang="ts">
    import { page } from '$app/state';
    import NavbarItem from '$lib/components/navbar/NavbarItem.svelte';

    let activeHash = $state('');
    let title = $state('');

    $effect(() => {
        activeHash = ['#home', '#destination', '#crew', '#technology'].includes(page.url.hash) ? page.url.hash : '#home';
        title = getTitle(activeHash);
    });

    // Get page title from the active hash, which is the name of the current section
    const getTitle = (activeHash: string): string => {
        let title = activeHash.replace('#', '');
        title = `${title.charAt(0).toLocaleUpperCase() + title.substring(1)}`;
        return title;
    };
</script>

<svelte:head>
    <title>{title}</title>
</svelte:head>

<nav>
    <NavbarItem href="#home" prefix="00" active={activeHash === '#home'}>Home</NavbarItem>
    <NavbarItem href="#destination" prefix="01" active={activeHash === '#destination'}>Destination</NavbarItem>
    <NavbarItem href="#crew" prefix="02" active={activeHash === '#crew'}>Crew</NavbarItem>
    <NavbarItem href="#technology" prefix="03" active={activeHash === '#technology'}>Technology</NavbarItem>
</nav>

<style>
    nav {
        display: flex;
        flex-direction: row;
        gap: 48px;
        padding: 0 64px 0 256px;
        background: rgba(var(--white-rgb), 0.05);
        box-shadow: 0 4px 30px rgba(0, 0, 0, 0.1);
        backdrop-filter: blur(40px);
        -webkit-backdrop-filter: blur(40px);
    }
</style>
