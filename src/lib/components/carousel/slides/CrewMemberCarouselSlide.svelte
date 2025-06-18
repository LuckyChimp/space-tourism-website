<script lang="ts">
    let {
        role,
        name,
        bio,
        image,
        isActive,
        textContainerOffsetHeight = $bindable(),
    }: { role: string; name: string; bio: string; image: string; isActive: boolean; textContainerOffsetHeight: number } = $props();
</script>

<div class="split-layout" class:active={isActive}>
    <div class="primary" bind:offsetHeight={textContainerOffsetHeight}>
        <div class="crew-member-text-container">
            <h4 class="crew-member-role">{role}</h4>
            <h3 class="crew-member-name">{name}</h3>
            <p class="crew-member-bio">{bio}</p>
        </div>
    </div>
    <div class="secondary">
        <img src={image} alt={name} class="crew-member-image" />
    </div>
</div>

<style>
    .split-layout {
        min-width: 100%;
        display: flex;
        justify-content: space-between;
        flex-wrap: wrap;
        gap: var(--400);
        padding-left: var(--section-padding-left);
        padding-right: var(--section-padding-right);
    }

    .primary {
        max-width: 600px;
        display: flex;
        flex-direction: column;
    }

    @media screen and (max-width: 850px) {
        .split-layout {
            padding: 0 var(--1000);
        }
    }

    @media screen and (max-width: 600px) {
        .split-layout {
            padding: 0 var(--800);
        }
    }

    .crew-member-text-container {
        height: 100%;
        display: flex;
        flex-direction: column;
        justify-content: center;
    }

    .crew-member-role {
        margin-bottom: var(--200);
        opacity: 0.5;
    }

    .crew-member-name {
        margin-bottom: var(--300);
    }

    .crew-member-bio {
        color: var(--light-blue);
    }

    .secondary {
        position: relative;
        display: flex;
        align-items: center;
        justify-content: center;
    }

    /* For bottom image blur */
    .secondary::after {
        content: '';
        position: absolute;
        height: var(--400);
        bottom: 0;
        left: 0;
        right: 0;
    }

    .crew-member-image {
        max-width: 100%;
        object-fit: contain;
        mask: linear-gradient(to bottom, #0b0e17 80%, transparent 100%);
    }

    /* Slide specific styles */
    /* -- 1st slide */
    @media screen and (max-width: 1497px) {
        :global(#crew .split-layout:nth-child(1)) {
            justify-content: center;
            gap: var(--1600);
        }

        :global(#crew .split-layout:nth-child(1) .primary) {
            text-align: center;
        }
    }

    /* -- 2nd slide */
    @media screen and (max-width: 1416px) {
        :global(#crew .split-layout:nth-child(2)) {
            justify-content: center;
            gap: var(--1600);
        }

        :global(#crew .split-layout:nth-child(2) .primary) {
            text-align: center;
        }
    }

    /* -- 3rd slide */
    @media screen and (max-width: 1532px) {
        :global(#crew .split-layout:nth-child(3)) {
            justify-content: center;
            gap: var(--1600);
        }

        :global(#crew .split-layout:nth-child(3) .primary) {
            text-align: center;
        }
    }

    /* -- 4th slide */
    @media screen and (max-width: 1558px) {
        :global(#crew .split-layout:nth-child(4)) {
            justify-content: center;
            gap: var(--1600);
        }

        :global(#crew .split-layout:nth-child(4) .primary) {
            text-align: center;
        }
    }
</style>
