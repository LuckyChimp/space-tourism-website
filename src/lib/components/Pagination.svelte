<script lang="ts">
    // Props
    let {
        type,
        orientation,
        activeIndex,
        length,
        onItemClick,
    }: {
        type: 'small' | 'largeWithNumbers';
        orientation: 'landscape' | 'portrait';
        activeIndex: number;
        length: number;
        onItemClick: (index: number) => void;
    } = $props();
</script>

<div
    class="pagination"
    class:type-small={type === 'small'}
    class:type-large-with-numbers={type === 'largeWithNumbers'}
    class:orientation-landscape={orientation === 'landscape'}
    class:orientation-portrait={orientation === 'portrait'}
>
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
        z-index: 1;
    }

    .pagination.type-small {
        gap: var(--500);
    }

    .pagination.type-large-with-numbers {
        gap: var(--400);
    }

    .pagination.orientation-landscape {
        flex-direction: row;
    }

    .pagination.orientation-portrait {
        flex-direction: column;
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

    @media screen and (max-width: 768px) {
        .pagination.type-small {
            gap: var(--200);
        }

        .pagination-item.type-small {
            width: var(--150);
            height: var(--150);
        }

        .pagination.type-large-with-numbers {
            gap: var(--200);
        }

        .pagination-item.type-large-with-numbers {
            width: var(--800);
            height: var(--800);
        }
    }

    @media screen and (max-width: 425px) {
        .pagination.type-large-with-numbers {
            gap: var(--200);
        }

        .pagination-item.type-large-with-numbers {
            width: var(--500);
            height: var(--500);
        }
    }
</style>
