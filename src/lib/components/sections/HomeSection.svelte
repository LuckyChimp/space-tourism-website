<script lang="ts">
    import { goto } from '$app/navigation';
</script>

<section id="home">
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
</section>

<style>
    #home {
        min-height: 100vh;
        display: flex;
        flex-direction: column-reverse;
        background-image: url('/images/home/background-home-desktop.jpg');
        background-size: cover;
        background-repeat: no-repeat;
        padding: calc(var(--500) + var(--1200) + var(--1600)) calc(var(--800) + var(--600) + var(--800)) var(--1600) calc(var(--800) + var(--600) + var(--800));
    }

    @media screen and (max-width: 1227px) {
        #home {
            background-image: url('/images/home/background-home-tablet.jpg');
            background-position: 50% 60%;
        }
    }

    @media screen and (max-width: 900px) {
        #home {
            padding: calc(var(--1200) + var(--1600)) var(--500) var(--1600);
        }
    }

    @media screen and (max-width: 869px) {
        #home {
            padding-top: calc(var(--1200) + var(--1600));
        }
    }

    @media screen and (max-width: 768px) {
        #home {
            padding: calc(var(--300) + var(--600) + var(--300) + var(--300)) var(--300) var(--300);
            flex-direction: initial;
        }
    }

    @media screen and (max-width: 425px) {
        #home {
            background-image: url('/images/home/background-home-mobile.jpg');
            background-position-x: 50%;
        }
    }

    .hero-section {
        width: 100%;
        display: flex;
        align-items: center;
        justify-content: space-between;
        gap: var(--800);
        flex-wrap: wrap;
    }

    @media screen and (max-width: 1227px) {
        .hero-section {
            justify-content: center;
            align-items: initial;
        }
    }

    .hero-section .hero-text {
        width: 540px;
        display: flex;
        flex-direction: column;
        gap: var(--300);
    }

    @media screen and (max-width: 1227px) {
        .hero-section .hero-text {
            align-items: center;
        }
    }

    .hero-section .hero-text p {
        color: var(--light-blue);
    }

    @media screen and (max-width: 1227px) {
        .hero-section .hero-text p {
            text-align: center;
        }
    }

    .hero-section .hero-button {
        width: 272px;
        height: 272px;
        border-radius: 50%;
        color: var(--dark-blue);
        cursor: pointer;
        transition: transform 100ms ease-out;
    }

    .hero-section .hero-button:hover {
        transform: scale(105%);
    }

    @media screen and (max-width: 768px) {
        .hero-section .hero-button {
            width: 144px;
            height: 144px;
        }
    }
</style>
