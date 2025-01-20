<script lang="ts">
    import { page } from '$app/state';
    import NavbarItem from '$lib/components/navbar/NavbarItem.svelte';
    import NavbarSlider from '$lib/components/navbar/NavbarSlider.svelte';

    const sections = ['Home', 'Destination', 'Crew', 'Technology'];
    const validHashes = sections.map((section) => `#${section.toLowerCase()}`);

    let activeHash = $state('#home');
    let activeItemIndex = $state(0);
    let itemWidths = $state(Array(sections.length).fill(0));

    $effect(() => {
        activeHash = validHashes.includes(page.url.hash) ? page.url.hash : '#home';
        activeItemIndex = validHashes.indexOf(activeHash);
    });

    const getTitle = (hash: string) => hash.slice(1).replace(/^\w/, (char) => char.toUpperCase());
</script>

<svelte:head>
    <title>{getTitle(activeHash)}</title>
</svelte:head>

<nav>
    {#each sections as section, index}
        <NavbarItem
            href={validHashes[index]}
            prefix={index.toLocaleString(undefined, { minimumIntegerDigits: 2 })}
            active={activeHash === validHashes[index]}
            bind:width={itemWidths[index]}
        >
            {section}
        </NavbarItem>
    {/each}
    <NavbarSlider {activeItemIndex} {itemWidths} />
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
