<script lang="ts">
    // Props
    let {
        type,
        activeIndex,
        length,
        onItemClick,
    }: { type: 'small' | 'largeWithNumbers'; activeIndex: number; length: number; onItemClick: (index: number) => void } = $props();
</script>

<div class="pagination" class:type-small={type === 'small'} class:type-large-with-numbers={type === 'largeWithNumbers'}>
    {#each { length }, index}
        <button
            onclick={() => onItemClick(index)}
            class="pagination-item"
            class:type-small={type === 'small'}
            class:type-large-with-numbers={type === 'largeWithNumbers'}
            class:active={activeIndex === index}
            aria-label="pagination item"
            >{#if type === 'largeWithNumbers'}<h4>{index + 1}</h4>{/if}</button
        >
    {/each}
</div>

<style>
    .pagination {
        display: flex;
        justify-content: center;
    }

    .pagination.type-small {
        flex-direction: row;
        gap: var(--500);
    }

    .pagination.type-large-with-numbers {
        flex-direction: column;
        gap: var(--400);
    }

    .pagination-item {
        border-radius: 50%;
        cursor: pointer;
        transition: all 200ms ease-out;
    }

    .pagination-item.type-small {
        width: var(--200);
        height: var(--200);
        background-color: rgba(var(--white-rgb), 0.17);
    }

    .pagination-item.type-large-with-numbers {
        width: var(--1000);
        height: var(--1000);
        background-color: transparent;
        border: 1px solid rgba(var(--white-rgb), 0.25);
    }

    .pagination-item.type-large-with-numbers.active {
        color: var(--dark-blue);
        border: none;
    }

    .pagination-item:hover {
        background-color: rgba(var(--white-rgb), 0.1);
    }

    .pagination-item.active {
        background-color: var(--white);
    }
</style>
