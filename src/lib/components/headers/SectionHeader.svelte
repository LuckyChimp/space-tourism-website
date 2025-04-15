<script lang="ts">
    let { sectionNumber, heading }: { sectionNumber: string; heading: string } = $props();
</script>

<div class="section-header">
    <h5 class="section-number">{sectionNumber}</h5>
    <h5 class="section-heading">{heading}</h5>
</div>

<style>
    .section-header {
        display: flex;
        align-items: center;
        gap: var(--300);
        padding-left: var(--padding-left, var(--section-padding-left));
        padding-right: var(--section-padding-right);
    }

    .section-header .section-number {
        font-weight: bold;
        letter-spacing: 4.7px;
        color: rgba(var(--white-rgb), 0.25);
    }

    .section-header .section-heading {
        color: var(--white);
    }

    @media screen and (max-width: 900px) {
        .section-header {
            padding-left: var(--500);
            padding-right: var(--500);
        }
    }

    @media screen and (max-width: 768px) {
        .section-header {
            padding-left: var(--300);
            padding-right: var(--300);
        }
    }

    @media screen and (max-width: 425px) {
        .section-header {
            justify-content: center;
        }
    }
</style>
