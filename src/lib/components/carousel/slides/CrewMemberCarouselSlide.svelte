<script lang="ts">
    let { role, name, bio, image }: { role: string; name: string; bio: string; image: string } = $props();
</script>

<div class="split-layout">
    <div class="primary">
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

    @media screen and (max-width: 886px) {
        .split-layout {
            padding: 0 var(--1000);
        }
    }

    @media screen and (max-width: 600px) {
        .split-layout {
            padding: 0 var(--800);
        }
    }

    .primary {
        max-width: 600px;
        display: flex;
        flex-direction: column;
    }

    @media screen and (max-width: 1497px) {
        .split-layout {
            justify-content: center;
        }

        .primary {
            text-align: center;
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
        mask-image: linear-gradient(to bottom, #0b0e17 80%, transparent 100%);
    }
</style>
