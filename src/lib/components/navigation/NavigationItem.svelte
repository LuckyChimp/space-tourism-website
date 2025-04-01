<script lang="ts">
    import type { Snippet } from 'svelte';

    // Props
    let {
        index,
        prefix,
        active,
        onClick,
        dimensions = $bindable({ width: 0, height: 0 }),
        children,
    }: {
        index: number;
        prefix: string | null;
        active: boolean;
        onClick: (index: number) => void;
        dimensions?: { width: number; height: number };
        children: Snippet;
    } = $props();
</script>

<div class="navbar-item" class:active bind:clientWidth={dimensions.width} bind:clientHeight={dimensions.height}>
    <button onclick={() => onClick(index)}>
        {#if prefix}<span class="number">{prefix}</span>{/if}
        <span class="text">{@render children()}</span>
    </button>
</div>

<style>
    button {
        color: var(--colorOfInactiveItems);
        background-color: transparent;
        cursor: pointer;
        transition: opacity 200ms ease-out;
    }

    button:hover {
        opacity: 0.6;
    }

    .navbar-item.active > button {
        color: var(--white);
    }

    span {
        font-family: var(--font-family-barlow-condensed);
        font-size: var(--200);
        letter-spacing: var(--25);
        text-transform: uppercase;
    }

    .number {
        font-weight: bold;
        margin-right: var(--150);
    }
</style>
