<script lang="ts">
	let quote:string = "";
	let author:string = "";
	let quotesData:Array<{quote: string, author: string}> = [];


	function initialSetup() {
		getQuotes;	// fetch the quote database
		getQuote;	// set the initial quote and author
	}

	function getQuotes() {
		console.log("running");
		fetch('https://gist.githubusercontent.com/camperbot/5a022b72e96c4c9585c32bf6a75f62d9/raw/e3c6895ce42069f0ee7e991229064f167fe8ccdc/quotes.json')
		.then(response => response.json())
		//.then(data => {
		//	console.log(data)
		//})
		.then(data => {
			quotesData = data.quotes;
			console.log(quotesData);
			console.log('whut?');
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
		console.log(`Random number selected: ${randomIndex}`)
		const chosenQuote = quotesData[randomIndex];
		quote =  chosenQuote.quote;
		author = chosenQuote.author;
	}


</script>

<svelte:head>
	<title>Random Quote Machine</title>
</svelte:head>
<svelte:window on:load={initialSetup}></svelte:window>

<main>


	<div id="quote-box">	</div>
	<div id="text">{quote}</div>
	<div id="author">{author}</div>
	<div id="buttons">
		<button id="new-quote" on:click={getQuote} >New Quote</button>
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