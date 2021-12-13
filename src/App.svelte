<script lang="ts">
	let quote:string = "";
	let author:string = "";
	let quotesData:Array<{quote: string, author: string}> = [];

	function getQuotes() {
		fetch('https://gist.githubusercontent.com/camperbot/5a022b72e96c4c9585c32bf6a75f62d9/raw/e3c6895ce42069f0ee7e991229064f167fe8ccdc/quotes.json')
		.then(response => response.json())
		.then(data => {
			quotesData = data.quotes;
			console.log(quotesData);
			getQuote();
		})
		.catch(error => {
			console.log(error);
		})
	}

	function getRandomNumber() {
		const randomNumber:number = Math.floor(Math.random() * quotesData.length);
		return randomNumber;
	}

	function getQuote() {
		const randomIndex = getRandomNumber();
		//console.log(`Random number selected: ${randomIndex}`)
		const chosenQuote = quotesData[randomIndex];
		quote =  chosenQuote.quote;
		author = chosenQuote.author;
	}

</script>

<svelte:head>
	<title>Random Quote Machine</title>
</svelte:head>
<svelte:window on:load={getQuotes}></svelte:window>

<main>
	<div id="quote-box">	
		<div id="text">{quote}</div>
		<div id="author">-- {author}</div>
		<div id="buttons">
			<button class="button" id="new-quote" on:click={getQuote} >New Quote</button>
			<a class="button" id="tweet-quote" href='https://www.twitter.com/intent/tweet?hashtags=quotes&text="{quote}"  --{author}  '>Tweet</a>	
		</div>
	</div>
	<div id="portfolio-link">
		<a id="portfolio-link-button" href="https://quargle.github.io/Portfolio/">Back To Portfolio Site</a>
	</div>
</main>

<style>

	:root {
		--black: #000000;
		--blue: #14213D;
		--yellow: #FCA311;
		--white: #E5E5E5; 
	}

	main {
		width: 100vw;
		height: 100vh;
		display: flex;
		flex-direction: column;
		justify-content: center;
		align-items: center;
		margin: 0;
		background-color: var(--blue);
	}

	#quote-box {
		border-radius: 5px;
		background-color: var(--white);
		width: 450px;
		padding: 40px 50px;
		height: auto;
		display: flex;
		flex-direction: column;
	}

	#text {
		width: 450px;
		height: auto;
		font-weight: 500;
		font-size: 1.75em;
	}

	#author {
		width: 450px;
		height: auto;
		padding-top: 20px;
		font-size: 1.25em;
		text-align: right;

	}

	#buttons {
		margin-top: 40px;
	}

	.button {
		border-radius: 5px;
		color: var(--black);
		border: 1px solid grey;
		width: auto;
		height: auto;
		background-color: white;
		box-sizing: border-box;
		padding: 10px 20px;
		margin: 10px;

	}

	#portfolio-link {
		background-color: var(--yellow);
		border-radius: 5px;
		margin: 40px;
		padding: 20px;
	}	
	#portfolio-link-button {
		color: var(--black);
	}
	

</style>