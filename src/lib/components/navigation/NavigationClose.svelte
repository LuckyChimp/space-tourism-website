<script lang="ts">
    import { navbar } from '$lib/globalStates.svelte';

    // Event listeners
    const onButtonClick = () => (navbar.isOpen = false);
</script>

<button onclick={onButtonClick}>
    <img src="/icons/icon-close.svg" alt="Menü schließen" />
</button>

<style>
    button {
        display: none;
        position: absolute;
        right: var(--400);
        background-color: transparent;
    }

    @media screen and (max-width: 768px) {
        button {
            display: initial;
        }
    }
</style>
