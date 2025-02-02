<script lang="ts">
    // Props
    let { activeIndex, length, onItemClick }: { activeIndex: number; length: number; onItemClick: (index: number) => void } = $props();
</script>

<div class="pagination">
    {#each { length }, index}
        <button onclick={() => onItemClick(index)} class="pagination-item" class:active={activeIndex === index} aria-label="pagination item"></button>
    {/each}
</div>

<style>
    .pagination {
        display: flex;
        gap: var(--500);

        padding-bottom: var(--padding-bottom, 0);
    }

    .pagination-item {
        width: var(--200);
        height: var(--200);
        border-radius: 50%;
        background-color: rgba(var(--white-rgb), 0.17);
        transition: background-color 200ms ease-out;
        cursor: pointer;
    }

    .pagination-item:hover {
        background-color: rgba(var(--white-rgb), 0.1);
    }

    .pagination-item.active {
        background-color: var(--white);
    }
</style>
