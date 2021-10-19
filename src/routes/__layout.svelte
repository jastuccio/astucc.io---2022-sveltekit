<script>
	import Header from '../../src/components/Header.svelte';
</script>

<div class=".container">
	<Header />
	<slot />
</div>

<style>
	.container {
		max-width: 600px;
		margin: 50px auto;
	}
</style>
