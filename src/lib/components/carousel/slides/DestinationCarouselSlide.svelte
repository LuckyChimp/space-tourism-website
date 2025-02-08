<script lang="ts">
    let { name, description, distance, travelTime, image }: { name: string; description: string; distance: string; travelTime: string; image: string } =
        $props();
</script>

<div class="two-columns">
    <div class="left-column">
        <img src={image} alt="moon" />
    </div>
    <div class="right-column">
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
</div>

<style>
    .two-columns {
        min-width: 100%;
        display: flex;
        align-items: center;
        padding-left: var(--section-padding-left);
        padding-right: var(--section-padding-right);
    }

    .left-column,
    .right-column {
        flex: 1;
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
