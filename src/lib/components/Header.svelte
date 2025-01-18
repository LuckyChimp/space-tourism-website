<script lang="ts">
    import Logo from '$lib/components/Logo.svelte';
    import Navbar from '$lib/components/navbar/Navbar.svelte';
</script>

<header>
    <Logo />
    <hr />
    <Navbar />
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
