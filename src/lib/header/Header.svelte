<script>
	import { fade } from 'svelte/transition';
	import { page } from '$app/stores';
	import { nav } from '../../data/nav.js'
	import sun from './sun.svg'
	import moon from './moon.svg'
	import menu from './menu.svg'
	import cancel from './cancel.svg'

	let theme = true;
	const toggleTheme = () => theme = !theme;

	let isOpen = false;
	const toggleIsOpen = () => isOpen = !isOpen;
</script>

<header>
	<!-- svelte-ignore component-name-lowercase -->
	<nav>
		<ul>
			{#each nav as navItem}
				<li class:active={$page.url.pathname === navItem.pathname}>
					<a sveltekit:prefetch href={navItem.pathname}>{navItem.text}</a>
				</li>
			{/each}
			<li>
				<a href="mailto:nathanjlardizabal@gmail.com">
					<span class="contact">contact</span>
				</a>
			</li>
		</ul>
	</nav>

	<article on:click={toggleTheme}>
		{#if theme}
			<img src={sun} alt="toggle light/dark" in:fade>
		{:else}
			<img src={moon} alt="toggle light/dark" in:fade>
		{/if}
	</article>

	<article class="menu" on:click={toggleIsOpen}>
		{#if isOpen}
			<img src={cancel} alt="close menu" in:fade>
		{:else}
			<img src={menu} alt="menu" in:fade>
		{/if}
	</article>
</header>

<style>
	header {
		position: sticky;
		top: 0;
		display: flex;
		justify-content: space-between;
		width: 100%;
		max-width: 80em;
		margin: 0 auto;
	}

	nav {
		display: flex;
		justify-content: center;
		--background: var(--primary-color);
	}

	ul {
		position: relative;
		padding: 0;
		margin: 0;
		height: 3em;
		display: flex;
		justify-content: center;
		align-items: center;
		list-style: none;
		background: var(--background);
		background-size: contain;
	}

	.menu {
		display: none;
	}

	li {
		position: relative;
		height: 100%;
	}

	li.active::before {
		--size: 6px;
		content: '';
		width: 0;
		height: 0;
		position: absolute;
		top: 0;
		left: calc(50% - var(--size));
		border: var(--size) solid transparent;
		border-top: var(--size) solid var(--accent-color);
	}
	
	.contact {
		color: var(--accent-color);
	}

	nav a {
		display: flex;
		height: 100%;
		align-items: center;
		padding: 0 1em;
		color: var(--heading-color);
		font-weight: 400;
		font-size: 1.2rem;
		text-transform: lowercase;
		letter-spacing: 0.02em;
		text-decoration: none;
		transition: 0.25s ease-in;
		position: relative;
	}

	nav a::after {
		content: "";
		position: absolute;
		left: 0;
		right: 0;
		bottom: 0.5rem;
		width: 75%;
		height: 4px;
		background: var(--accent-color);
		transform: scale(0);
		transform-origin: left;
		transition: 0.25s ease-in;
		margin: 0 auto;
		text-align: center;
	}

	nav a:hover::after {
		transform: scale(1);
	}

	a:hover {
		color: var(--accent-color);
	}

	article {
		cursor: pointer;
	}

	img {
		padding: 1rem;
		height: 2rem;
		width: 2rem;
		transition: 0.5s ease-in;
	}

	img:hover {
		transform: scale(1.3);
	}

	/* media queries */
	@media (max-width: 60em) {
		header {
			justify-content: flex-end;
			inset: 0 0 0 40%;
			background: hsl(0 0% 100% / 0.1);
			/* backdrop-filter: blur(50rem); */
		}

		ul {
			display: none;
		}

		.menu {
			display: flex;
		}
	}


</style>
