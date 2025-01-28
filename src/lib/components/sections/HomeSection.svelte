<script lang="ts">
    import { goto } from '$app/navigation';
</script>

<div id="home">
    <div class="hero-section">
        <div class="hero-text">
            <h5>So, you want to travel to</h5>
            <h1>Space</h1>
            <p>
                Let's face it; if you want to go to space, you might as well genuinely go to outer space and not hover kind of on the edge of it. Well sit back,
                and relax because we'll give you a truly out of this world experience!
            </p>
        </div>
        <button onclick={() => goto('#destination')} class="hero-button"><h4>Explore</h4></button>
    </div>
</div>

<style>
    #home {
        height: 100vh;
        display: flex;
        flex-direction: column-reverse;
        background-image: url('images/home/background-home-desktop.jpg');
        background-size: cover;
        background-repeat: no-repeat;
    }

    .hero-section {
        width: 100%;
        display: flex;
        align-items: center;
        justify-content: space-between;
        padding: 0 calc(var(--800) + var(--600) + var(--800)) var(--1600) calc(var(--800) + var(--600) + var(--800));
    }

    .hero-section .hero-text {
        width: 540px;
        display: flex;
        flex-direction: column;
        gap: var(--300);
    }

    .hero-section .hero-button {
        width: 272px;
        height: 272px;
        border-radius: 50%;
        cursor: pointer;
        transition: transform ease-out 100ms;
    }

    .hero-section .hero-button:hover {
        transform: scale(105%);
    }
</style>
