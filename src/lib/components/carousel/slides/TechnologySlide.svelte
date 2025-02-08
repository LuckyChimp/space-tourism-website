<script lang="ts">
    // Props
    let { name, description, image }: { name: string; description: string; image: string } = $props();
</script>

<div class="two-columns">
    <div class="left-column">
        <h4 class="technology-heading">The terminology...</h4>
        <h3 class="technology-name">{name}</h3>
        <p class="technology-description">{description}</p>
    </div>
    <div class="right-column">
        <img src={image} alt={name} class="technology-image" />
    </div>
</div>

<style>
    .two-columns {
        min-height: 100%;
        display: flex;
        justify-content: space-between;
        align-items: center;
        gap: var(--400);
    }

    .left-column {
        display: flex;
        flex-flow: column nowrap;
        justify-content: center;
        gap: var(--200);
    }

    .technology-heading {
        opacity: 0.5;
    }

    .technology-description {
        color: var(--light-blue);
    }
</style>
