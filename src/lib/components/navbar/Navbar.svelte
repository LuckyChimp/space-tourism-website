<script lang="ts">
    import { page } from '$app/state';
    import NavbarItem from '$lib/components/navbar/NavbarItem.svelte';

    let slider: HTMLDivElement;

    let activeHash = $state('');
    let title = $state('');
    let itemWidths = $state([0, 0, 0, 0]);

    $effect(() => {
        activeHash = ['#home', '#destination', '#crew', '#technology'].includes(page.url.hash) ? page.url.hash : '#home';
        title = getTitle(activeHash);
        setTimeout(() => {
            // Move slider according to the current section
            const index = ['Home', 'Destination', 'Crew', 'Technology'].indexOf(title);
            slider.style.width = `${itemWidths[index]}px`;
            const calcXOffset = () => {
                let xOffset = index * 48; // = gap between nav items
                for (var i = 0; i < index; i++) {
                    xOffset += itemWidths[i]; // = width of previous nav items
                }
                return xOffset;
            };
            slider.style.transform = `translateX(${calcXOffset()}px)`;
        }, 10);
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
    <NavbarItem href="#home" prefix="00" active={activeHash === '#home'} bind:width={itemWidths[0]}>Home</NavbarItem>
    <NavbarItem href="#destination" prefix="01" active={activeHash === '#destination'} bind:width={itemWidths[1]}>Destination</NavbarItem>
    <NavbarItem href="#crew" prefix="02" active={activeHash === '#crew'} bind:width={itemWidths[2]}>Crew</NavbarItem>
    <NavbarItem href="#technology" prefix="03" active={activeHash === '#technology'} bind:width={itemWidths[3]}>Technology</NavbarItem>
    <div class="slider" bind:this={slider}></div>
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

    nav:has(:global(.navbar-item.active:hover)) .slider {
        background-color: rgba(var(--white-rgb), 0.6);
    }

    nav .slider {
        height: 3px;
        position: absolute;
        bottom: 0;
        background-color: var(--white);
        transition: all ease-out 300ms;
    }
</style>
