<script lang="ts">
    let {
        index,
        prefix,
        active,
        onClick,
        width = $bindable(),
        children,
    }: {
        index: number;
        prefix: string | null;
        active: boolean;
        onClick: (index: number) => void;
        width?: number;
        children?: any;
    } = $props();
</script>

<div class="navbar-item" class:active bind:clientWidth={width}>
    <button onclick={() => onClick(index)}>
        {#if prefix}<span class="number">{prefix}</span>{/if}
        <span class="text">{@render children()}</span>
    </button>
</div>

<style>
    button {
        color: var(--colorOfInactiveItems, var(--white));
        background-color: transparent;
        cursor: pointer;
        transition: color ease-out 200ms;
    }

    button:hover {
        color: rgba(var(--white-rgb), 0.6);
    }

    .navbar-item.active > button {
        color: var(--white);
    }

    span {
        font-family: var(--font-family-barlow-condensed);
        font-size: 16px;
        letter-spacing: 2px;
        text-transform: uppercase;
    }

    .number {
        font-weight: bold;
        margin-right: 12px;
    }
</style>
