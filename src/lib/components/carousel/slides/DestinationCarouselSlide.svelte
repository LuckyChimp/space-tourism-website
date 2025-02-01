<script lang="ts">
    let { name, description, distance, travelTime, active }: { name: string; description: string; distance: string; travelTime: string; active: boolean } =
        $props();
</script>

<div class="destination-carousel-slide" class:active>
    <h2 class="destination-name">{name}</h2>
    <p class="destination-description">{description}</p>
    <hr />
    <div class="distance-travel-time-container">
        <div class="distance-container">
            <small>Avg. distance</small>
            <h6>{distance}</h6>
        </div>
        <div class="travel-time-container">
            <small>Est. travel time</small>
            <h6>{travelTime}</h6>
        </div>
    </div>
</div>

<style>
    .destination-carousel-slide {
        min-width: 100%;
    }

    .destination-name {
        margin: var(--500) 0 var(--200) 0;
    }

    .destination-description,
    small {
        color: var(--light-blue);
    }

    hr {
        margin: var(--500) 0;
    }

    .distance-travel-time-container {
        display: flex;
        gap: var(--300);
    }

    .distance-travel-time-container > div {
        flex: 1;
    }

    h6 {
        margin-top: var(--150);
    }
</style>
