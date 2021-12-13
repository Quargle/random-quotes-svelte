<script lang="ts">
//	import { fade } from 'svelte/transition';

	let quote:string = "";
	let author:string = "";
	let quotesData:Array<{quote: string, author: string}> = [];
	const colors:Array<string> = [
		"#264653",
		"#2a9d8f",
		"#e9c46a",
		"#f4a261",
		"#e76f51",		
		"#001219",
		"#005f73",
		"#0a9396",
		"#94d2bd",
		"#e9d8a6",
		"#ee9b00",
		"#ca6702",
		"#bb3e03",
		"#ae2012",
		"#9b2226"
		];

	
	
	// const colors:Array<string> = [
	//   '#16a085',
	//   '#27ae60',
	//   '#2c3e50',
	//   '#f39c12',
	//   '#e74c3c',
	//   '#9b59b6',
	//   '#FB6964',
	//   '#342224',
	//   '#472E32',
	//   '#BDBB99',
	//   '#77B1A9',
	//   '#73A857'
	// ];
	let backgroundColor:string = '#14213D'
	$: cssVarStyles = `--background-color:${backgroundColor}`;

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

	function getRandomNumber(max:number) {
		const randomNumber:number = Math.floor(Math.random() * max);
		return randomNumber;
	}

	function getQuote() {
		const randomIndex = getRandomNumber(quotesData.length);
		//console.log(`Random number selected: ${randomIndex}`)
		const chosenQuote = quotesData[randomIndex];
		quote =  chosenQuote.quote;
		author = chosenQuote.author;
		backgroundColor = colors[getRandomNumber(colors.length)];
	}
</script>

<svelte:head>
	<title>Random Quote Machine</title>
</svelte:head>
<svelte:window on:load={getQuotes} />

<main class="color-transition" style="{cssVarStyles}">
	<div id="quote-box">	
		<div id="text">{quote}</div>
		<div id="author">-- {author}</div>
		<div id="buttons">
			<button 
				class="button color-transition" 
				id="new-quote" 
				on:click={getQuote} 
				style="{cssVarStyles}">
				New Quote
			</button>
			<a class="button" id="tweet-quote" href='https://www.twitter.com/intent/tweet?hashtags=quotes&text="{quote}"  --{author}  '>Tweet</a>	
		</div>
	</div>
	<div id="portfolio-link">
		<a id="portfolio-link-button" href="https://quargle.github.io/Portfolio/" target="_blank">Portfolio</a>
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
		max-width: 100%;
		max-height: 100%;
		padding: 40px 50px;
		height: auto;
		display: flex;
		flex-direction: column;
		box-sizing: border-box;
	}

	#text {
		width: auto;
		height: auto;
		font-weight: 500;
		font-size: 1.75em;
	}

	#author {
		width: auto;
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
		color: white;
		width: auto;
		height: auto;
		background-color: white;
		box-sizing: border-box;
		padding: 10px 20px;
		margin: 10px;

	}

	#new-quote {
		border: none;
		/*background-color: var(--blue);*/
	}

	#tweet-quote {
		background-color: rgb(29, 155, 240);
		border: none;
	}

	#portfolio-link {
		margin-top: 40px;
	}

	#portfolio-link-button {
		color: var(--white);
		Padding: 30px;
	}

	.color-transition {
		background-color: var(--background-color); 
		transition-property: background-color; 
		transition-duration: 4s;
	}
</style>