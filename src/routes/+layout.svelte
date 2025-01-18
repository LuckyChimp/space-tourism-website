<script lang="ts">
	import Header from '$lib/components/Header.svelte';
	import '@fontsource/barlow';
	import '@fontsource/barlow-condensed';
	import '@fontsource/bellefair';
	// global.css with variables etc. is inherited by all pages of this website
	import '$lib/styles/global.css';

	let { children } = $props();
</script>

<Header />
{@render children()}
