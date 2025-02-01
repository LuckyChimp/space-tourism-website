<script lang="ts">
    let { sectionNumber, heading }: { sectionNumber: string; heading: string } = $props();
</script>

<div class="section-header">
    <p class="section-number">{sectionNumber}</p>
    <h5 class="section-heading">{heading}</h5>
</div>

<style>
    .section-header {
        display: flex;
        align-items: center;
        gap: var(--300);
    }

    .section-header .section-number {
        font-family: var(--font-family-barlow-condensed);
        font-size: 28px;
        font-weight: bold;
        letter-spacing: 4.7px;
        color: rgba(var(--white-rgb), 0.25);
    }

    .section-header .section-heading {
        color: var(--white);
    }
</style>
