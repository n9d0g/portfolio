<script>
  export let link;
  export let svg;
  export let alt;
</script>

<li>
  <a href={link} target="_blank">
    <img src={svg} alt={alt}>
  </a>
</li>

<style>
	li {
		display: flex;
		justify-content: center;
		align-items: center;
	}

	img {
		padding: 0 1rem;
		height: 1.5rem;
		width: 1.5rem;
		transition: .1s ease-in;
	}

	img:hover {
		transform: scale(1.2);
	}

	@media (max-width: 60em) {
		img {
			height: 1.2rem;
			width: 1.2rem;
		}
	}
</style>
