<script lang="ts">
    let {
        href,
        prefix = '',
        active = false,
        children,
    }: {
        href: string;
        prefix: string;
        active: boolean;
        children: any;
    } = $props();
</script>

<div class="navbar-item" class:active>
    <a {href}>
        <span class="number">{prefix}</span>
        <span class="text">{@render children()}</span>
    </a>
</div>

<style>
    .navbar-item {
        height: 96px;
        padding: 40px 0;
    }

    .navbar-item.active {
        border-bottom: 3px solid var(--white);
        transition: border-bottom-color ease-out 200ms;
    }

    .navbar-item.active:has(a:hover) {
        border-bottom-color: rgba(var(--white-rgb), 0.6);
    }

    a {
        color: var(--white);
        text-decoration: none;
        transition: color ease-out 200ms;
    }

    a:hover {
        color: rgba(var(--white-rgb), 0.6);
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
