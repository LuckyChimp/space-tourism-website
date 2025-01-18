<script lang="ts">
	// global.css with variables etc. is inherited by all pages of this website
	import '$lib/styles/global.css';

	let { children } = $props();
</script>

<div id="page">
	<nav></nav>
	{@render children()}
</div>

<style>
	#page {
		width: 100vw;
		min-height: 100vh;
		background-image: url('home/background-home-desktop.jpg');
		background-size: 100% auto;
		background-repeat: no-repeat;
	}
</style>
