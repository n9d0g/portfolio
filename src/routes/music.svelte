<script context="module">
	import { browser, dev } from '$app/env';
	import { fade } from 'svelte/transition';

	// we don't need any JS on this page, though we'll load
	// it in dev so that we get hot module replacement...
	export const hydrate = dev;

	// ...but if the client-side router is already loaded
	// (i.e. we came here from elsewhere in the app), use it
	export const router = browser;

	// since there's no dynamic data here, we can prerender
	// it so that it gets served as a static asset in prod
	export const prerender = true;
</script>

<svelte:head>
	<title>n9 | music</title>
</svelte:head>

<div class="content" in:fade={{ duration: 1000 }}>
	<h1>dim7</h1>
</div>

<style>
	h1 {
		color: var(--accent-color);
	}
	.content {
		width: 100%;
		max-width: var(--column-width);
		margin: var(--column-margin-top) auto 0 auto;
	}

	@media (max-width: 60em) {
		.content {
			margin: 0 auto;
			justify-content: flex-start;
		}
	}
</style>
