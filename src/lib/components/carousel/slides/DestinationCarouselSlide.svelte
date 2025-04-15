<script lang="ts">
    let { name, description, distance, travelTime, image }: { name: string; description: string; distance: string; travelTime: string; image: string } =
        $props();
</script>

<div class="split-layout">
    <div class="primary">
        <img src={image} alt="moon" />
    </div>
    <div class="secondary">
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
    .split-layout {
        min-width: 100%;
        display: flex;
        align-items: center;
        flex-wrap: wrap;
        gap: var(--400);
        padding-left: var(--section-padding-left);
        padding-right: var(--section-padding-right);
    }

    .primary,
    .secondary {
        flex: 1;
    }

    .destination-name {
        margin: calc(var(--400) + var(--500)) 0 var(--200) 0;
    }

    .destination-description,
    small {
        color: var(--light-blue);
    }

    hr {
        margin: var(--500) 0;
    }

    .distance-travel-time-container {
        width: 100%;
        display: flex;
        gap: var(--300);
        flex-wrap: wrap;
    }

    .distance-travel-time-container > div {
        flex: 1;
    }

    h6 {
        margin-top: var(--150);
    }

    @media screen and (max-width: 1276px) {
        .split-layout {
            flex-direction: column;
            padding: 0 var(--1600);
            gap: calc(var(--1000));
        }

        .primary,
        .secondary {
            flex: initial;
        }

        .secondary {
            display: flex;
            flex-flow: column;
            align-items: center;
            margin-top: calc(var(--400) + var(--300));
        }

        .destination-name {
            margin-top: 0;
        }

        .destination-description {
            text-align: center;
        }

        hr {
            width: 100%;
        }

        .distance-travel-time-container {
            justify-content: space-evenly;
        }

        .distance-travel-time-container > * {
            flex: initial !important;
            text-align: center;
        }
    }

    @media screen and (max-width: 768px) {
        .primary img {
            width: 300px;
            height: 300px;
        }
    }

    @media screen and (max-width: 636px) {
        .split-layout {
            padding: 0 var(--800);
        }
    }

    @media screen and (max-width: 425px) {
        .primary img {
            width: 150px;
            height: 150px;
        }
    }
</style>
