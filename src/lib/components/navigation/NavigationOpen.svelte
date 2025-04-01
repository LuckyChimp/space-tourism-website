<script lang="ts">
    import { navbar } from '$lib/globalStates.svelte';

    // Event listeners
    const onButtonClick = () => (navbar.isOpen = true);
</script>

<button onclick={onButtonClick}>
    <img src="/icons/icon-hamburger.svg" alt="Menü öffnen" />
</button>

<style>
    button {
        display: none;
        position: absolute;
        top: calc(var(--300) + 12px);
        right: 0;
        background-color: transparent;
    }

    @media screen and (max-width: 768px) {
        button {
            display: initial;
        }
    }
</style>
