<script>
	import { navigating } from '$app/state';
	import { cubicOut } from 'svelte/easing';
	import { Tween } from 'svelte/motion';
	import { fade } from 'svelte/transition';
	// We use Tween to animate the  value change.
	const p = new Tween(0.35, {
		duration: 200,
		easing: cubicOut
	});
	function increase() {
		const progressLeft = 1 - p.current;
		p.set(p.current + progressLeft * 0.01);
		if (p.current > 1) {
			p.set(1);
		}
		if (navigating.complete) {
			const waitTime = Math.round(Math.random() * 250) + 50;
			setTimeout(increase, waitTime);
		} else {
			p.set(1);
			setTimeout(() => p.set(0), 50);
		}
	}
	$effect(() => {
		if (navigating.complete) {
			increase();
		}
	});
</script>

{#if navigating.complete || true}
	<!-- we use the fade animation from svelte/transition  and use the tween.current for the value -->
	<progress value={p.current} in:fade={{ duration: 300 }} out:fade={{ duration: 300 }}> </progress>
{/if}

<style>
	progress {
		position: fixed;
		top: 0;
		z-index: 99999;
		left: 0;
		height: 4px;
		width: 100%;
		appearance: none;
		border: none;
		outline: none; /* firefox has a default outline */
	}
	progress::-webkit-progress-bar {
		background-color: transparent;
	}
	progress::-webkit-progress-value {
		background-color: red;
	}
	progress::-moz-progress-bar {
		background-color: red;
	}
</style>
