<script lang="ts">
	import NavigationProgress from '$lib/components/NavigationProgress.svelte';

	let { children } = $props();
</script>

<NavigationProgress />
<header>
	<h1>Sveltekit Navigation Progress</h1>
	<nav>
		<a href="/">Home</a>
		<a href="/services">Services</a>
	</nav>
</header>
{@render children()}
