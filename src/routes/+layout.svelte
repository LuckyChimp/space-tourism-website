<script lang="ts">
	import '@fontsource/barlow';
	import '@fontsource/barlow-condensed';
	import '@fontsource/bellefair';
	// global.css with variables etc. is inherited by all pages of this website
	import '$lib/styles/global.css';

	let { children } = $props();
</script>

{@render children()}
