<script lang="ts">
    // Props
    let {
        name,
        description,
        image,
        orientation,
        imageHeight = $bindable(),
    }: { name: string; description: string; image: string; orientation: 'landscape' | 'portrait'; imageHeight: number } = $props();
</script>

<div class="split-layout" class:orientation-landscape={orientation === 'landscape'} class:orientation-portrait={orientation === 'portrait'}>
    <div class="primary">
        <h4 class="technology-heading">The terminology...</h4>
        <h3 class="technology-name">{name}</h3>
        <p class="technology-description">{description}</p>
    </div>
    <img src={image} alt={name} class="secondary" bind:clientHeight={imageHeight} />
</div>

<style>
    .split-layout {
        display: flex;
        justify-content: space-between;
        align-items: center;
        gap: var(--400);
    }

    .split-layout.orientation-landscape {
        min-width: 100%;
        flex-direction: column-reverse;
    }

    .split-layout.orientation-portrait {
        min-height: 100%;
    }

    .primary {
        display: flex;
        flex-flow: column nowrap;
        justify-content: center;
        gap: var(--200);
    }

    .split-layout.orientation-landscape .primary {
        mask: linear-gradient(to left, transparent 0%, var(--white) 20% 80%, transparent 100%);
    }

    @media screen and (max-width: 1336px) {
        .split-layout {
            flex-direction: column;
            gap: calc(var(--1200) * 2);
        }

        .primary {
            width: 100%;
            align-items: center;
            padding-left: var(--section-padding-left);
            padding-right: var(--section-padding-right);
        }

        .technology-name {
            text-align: center;
        }

        .technology-description {
            text-align: center;
        }
    }

    @media screen and (max-width: 850px) {
        .primary {
            padding: 0 var(--1000);
        }
    }

    @media screen and (max-width: 768px) {
        .split-layout {
            gap: var(--1600);
        }
    }

    @media screen and (max-width: 600px) {
        .primary {
            padding: 0 var(--800);
        }
    }

    @media screen and (max-width: 425px) {
        .split-layout {
            gap: var(--1200);
        }
    }

    .technology-heading {
        opacity: 0.5;
    }

    .technology-description {
        color: var(--light-blue);
    }

    .secondary {
        width: 100%;
    }
</style>
