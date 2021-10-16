<script>
	import Nav from 'src/components/Nav.svelte';
</script>

<div class="container">
	<Nav />
	<slot />
</div>

<style>
	.container {
		max-width: 600px;
		margin: 50px auto;
	}
</style>
