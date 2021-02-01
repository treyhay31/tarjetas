<script>
	import Bonus from "./components/bonus.svelte"
	const months = [
		"January", 
		"February", 
		"March", 
		"April", 
		"May",
		"June",
		"July",
		"August",
		"September", 
		"October", 
		"November", 
		"December"
	]
	const quarters = [
		"Q1", "Q1", "Q1",
		"Q2", "Q2", "Q2",
		"Q3", "Q3", "Q3",
		"Q4", "Q4", "Q4",
	]
	let date = new Date();
	const m = date.getMonth();
	let quarter = quarters[m];
	const getNextQuarter = () => {
		month = "any month in"
		quarter = nextQuarter()
	}
	const nextQuarter = () => {
		const [_, qs] = quarter
		const q = parseInt(qs)
		if (q+1 > 4) {
			return `Q${1}`
		} else {
		  return `Q${q + 1}`
		}
	}
	$: theNextQuarter = nextQuarter() 
	let month = months[m];
	const year = date.getFullYear();
	const bonuses = {
    chase: {
			Q1: ["wholesale","internet/cable/phone","streaming"],
			Q2: ["unknown"],
			Q3: ["unknown"],
			Q4: ["unknown"]
		},
		discover:{
			Q1: ["grocery","walgreens & CVS"],
			Q2: ["Gas Stations", "Wholesale Clubs", "Select Streaming Services"],
			Q3: ["Restaurants","Paypal"],
			Q4: ["Amazon","Walmart","Target"]
		},
		amexBcp: ["streaming", "grocery"],
		chaseSapphire5: ["lyft"],
		chaseSapphire2: ["travel", "dining"],
		chaseFreedom3: ["dining", "drugstore"], 
		boa2: ["costco/wholesale"],
		boa3: [
			"online shopping","dining","drug store","gas","travel","home improvement"
		],
		citi4: ["gas"],
		citi3: ["dining", "travel"],
		citi2: ["costco"],
		amazon: ["amazon"]
	};
	const url = "https://www.nerdwallet.com/credit-cards"
</script>
<style>
	.time {
		display: grid;
		grid-template-columns: 3fr 1fr;
		justify-items: center;
	}
	
	.six-percent::before {
		content:'6%';
		position: absolute;
		top: .4rem;
		right: .4rem;
	}
	.five-percent::before {
		content:'5%';
		position: absolute;
		top: .4rem;
		right: .4rem;
	}
	.four-percent::before {
		content:'4%';
		position: absolute;
		top: .4rem;
		right: .4rem;
	}
	.three-percent::before {
		content:'3%';
		position: absolute;
		top: .4rem;
		right: .4rem;
	}
	.six-percent {
		background: linear-gradient(70deg, #fefefe, #ffadd2);
	}
	.five-percent {
		background: linear-gradient(70deg, #fefefe, #b2faf5);
	}
	.four-percent {
		background: linear-gradient(70deg, #fefefe, #ffd685);
	}
	.three-percent {
		background: linear-gradient(70deg, #fefefe, #beb2c8);
	}
	.bonus {
		border-radius: 3px;
		padding: 1rem;
		margin: .5rem .2rem;
		position: relative
	}
	main {
		font-size: 1.5rem;
	}
	button {
		outline: none;
		border: none;
		border-radius: 2rem;
		background-color: #b2faf5;
		font-weight: 500;
		height: 3rem;
		padding: .1rem 2rem;
		transform: translateY(1.8rem);
	}
</style>
<main>
	<section class="time">
		<h1>It's {month} ({quarter}) {year}</h1>
		<button on:click={getNextQuarter}>
				{theNextQuarter} &gt;
		</button>
	</section>
	<section class="bonus six-percent">
		<Bonus cardName="AMEX Blue Cash Preferred" {url} bonuses={bonuses.amexBcp} />
	</section>
	<section class="bonus five-percent">
		<Bonus cardName="Chase" url="https://www.chasebonus.com/" bonuses={bonuses["chase"][quarter]} />
		<Bonus cardName="Discover" url="https://www.discover.com/credit-cards/cashback-bonus/cashback-calendar.html" bonuses={bonuses["discover"][quarter]} />	
		<Bonus cardName="Amazon" {url} bonuses={bonuses.amazon} />
	</section>
	<section class="bonus four-percent">
		<Bonus cardName="Citi" {url} bonuses={bonuses.citi4} />
	</section>
	<section class="bonus three-percent">
		<Bonus cardName="Citi" {url} bonuses={bonuses.citi3} />
		<Bonus cardName="Rotating BOA" {url} bonuses={bonuses.boa3} />
	</section>
</main>
