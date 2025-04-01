<script lang="ts">
    import { goto } from '$app/navigation';
    import Logo from '$lib/components/Logo.svelte';
    import Navbar from '$lib/components/navigation/NavigationMenu.svelte';
    import NavigationOpen from '$lib/components/navigation/NavigationOpen.svelte';

    // Props
    let { activeNavbarItemIndex, navbarSections }: { activeNavbarItemIndex: number; navbarSections: string[] } = $props();

    // Event listeners
    const onNavbarItemClick = (index: number) => goto(`#${navbarSections[index].toLowerCase()}`);
</script>

<header>
    <Logo />
    <hr />
    <Navbar
        activeIndex={activeNavbarItemIndex}
        context="website"
        sections={navbarSections}
        onItemClick={onNavbarItemClick}
        --itemGap="var(--600)"
        --height="var(--1200)"
        --padding="0 var(--800) 0 var(--3200)"
        --colorOfInactiveItems="var(--white)"
    />
    <NavigationOpen />
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

    @media screen and (max-width: 869px) {
        header {
            top: 0;
            left: var(--500);
        }
    }

    @media screen and (max-width: 768px) {
        header {
            left: var(--300);
            right: var(--300);
        }
    }

    hr {
        width: 50%;
        position: absolute;
        left: calc(var(--600) + var(--800));
        z-index: 1;
    }

    @media screen and (max-width: 1600px) {
        hr {
            width: 40%;
        }
    }

    @media screen and (max-width: 1350px) {
        hr {
            width: 30%;
        }
    }

    @media screen and (max-width: 1150px) {
        hr {
            display: none;
        }
    }
</style>
