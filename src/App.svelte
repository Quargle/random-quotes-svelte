<script lang="ts">
	let quote:string = "";
	let author:string = "";


</script>

<svelte:head>
	<title>Random Quote Machine</title>
</svelte:head>

<main>


	<div id="quote-box">	</div>
	<div id="text"></div>
	<div id="author"></div>
	<div id="buttons">
		<button id="new-quote">New Quote</button>
		<a id="tweet-quote" href="https://www.twitter.com/intent/tweet">Tweet</a>	
	</div>


</main>

<style>
	main {
		text-align: center;
		padding: 1em;
		max-width: 240px;
		margin: 0 auto;
	}

	h1 {
		color: #ff3e00;
		text-transform: uppercase;
		font-size: 4em;
		font-weight: 100;
	}

	@media (min-width: 640px) {
		main {
			max-width: none;
		}
	}
</style>