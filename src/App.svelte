<script>
	import Bonus from "./components/bonus.svelte";
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
		"December",
	];
	const quarters = [
		"Q1",
		"Q1",
		"Q1",
		"Q2",
		"Q2",
		"Q2",
		"Q3",
		"Q3",
		"Q3",
		"Q4",
		"Q4",
		"Q4",
	];
	let date = new Date();
	const m = date.getMonth();
	let quarter = quarters[m];
	const getNextQuarter = () => {
		month = "any month in";
		quarter = nextQuarter(quarter);
	};
	const nextQuarter = (qtr) => {
		const [_, qs] = qtr;
		const q = parseInt(qs);
		if (q + 1 > 4) {
			return `Q${1}`;
		} else {
			return `Q${q + 1}`;
		}
	};
	$: theNextQuarter = nextQuarter(quarter);
	let month = months[m];
	const year = date.getFullYear();
	const bonuses = {
		chase: {
			Q1: ["wholesale", "internet/cable/phone", "streaming"],
			Q2: ["gas stations", "home improvement"],
			Q3: ["Grocery"],
			Q4: ["unknown"],
		},
		discover: {
			Q1: ["grocery", "walgreens & CVS"],
			Q2: ["Gas Stations", "Wholesale Clubs", "Select Streaming Services"],
			Q3: ["Restaurants", "Paypal"],
			Q4: ["Amazon", "Walmart", "Target"],
		},
		amexBcp: ["streaming", "grocery"],
		chaseSapphire5: ["lyft"],
		chaseSapphire2: ["travel", "dining"],
		chaseFreedom3: ["dining", "drugstore"],
		boa2: ["costco/wholesale"],
		boa3: [
			"online shopping",
			"dining",
			"drug store",
			"gas",
			"travel",
			"home improvement",
		],
		citiCash: [
			"Restaurants",
			"gas stations",
			"grocery stores",
			"select travel/transit/streaming",
			"drugstores",
			"home improvement stores",
			"fitness clubs",
			"live entertainment",
		],
		citi4: ["gas"],
		citi3: ["dining", "travel"],
		citi2: ["costco"],
		amazon: ["amazon"],
	};
	const url = "https://www.nerdwallet.com/credit-cards";
</script>

<main>
	<section class="time">
		<h1>It's {month} ({quarter}) {year}</h1>
		<button on:click={getNextQuarter}>
			{theNextQuarter} &gt;
		</button>
	</section>
	<section class="bonus six-percent">
		<Bonus
			cardName="AMEX Blue Cash Preferred"
			{url}
			bonuses={bonuses.amexBcp}
		/>
	</section>
	<section class="bonus five-percent">
		<Bonus
			cardName="Chase"
			url="https://www.chasebonus.com/"
			bonuses={bonuses["chase"][quarter]}
		/>
		<Bonus
			cardName="Discover"
			url="https://www.discover.com/credit-cards/cashback-bonus/cashback-calendar.html"
			bonuses={bonuses["discover"][quarter]}
		/>
		<Bonus
			cardName="Amazon"
			url="https://www.amazon.com/Amazon-Rewards-Visa-Signature-Card/dp/B007URFTYI"
			bonuses={bonuses.amazon}
		/>
		<Bonus
			cardName="CitiCash (rotating)"
			url="https://citicards.citi.com/usc/LPACA/Citi/Cards/CustomCash/ps/index.html?cmp=knc|acquire|2006|CARDS|Google|BR&gclid=CjwKCAjwmK6IBhBqEiwAocMc8qJ9upbf9SnM_wkdgsNpPjFUMckCi2Xp1d2sJxznzlXTi7JHlpBnMRoCKGEQAvD_BwE&gclsrc=aw.ds&BT_TX=1&ProspectID=323482389D9E403A8DC4CA38944C67AE"
			bonuses={bonuses.citiCash}
		/>
	</section>
	<section class="bonus four-percent">
		<Bonus
			cardName="Citi"
			url="https://www.costco.com/credit-card.html"
			bonuses={bonuses.citi4}
		/>
	</section>
	<section class="bonus three-percent">
		<Bonus
			cardName="Citi"
			url="https://www.costco.com/credit-card.html"
			bonuses={bonuses.citi3}
		/>
		<Bonus
			cardName="Rotating BOA"
			url="https://www.bankofamerica.com/credit-cards/products/cash-back-credit-card/?campaign=4047600~5B~en_US"
			bonuses={bonuses.boa3}
		/>
	</section>
</main>

<style>
	:root {
		--six: #ffadd2;
		--five: #b2faf5;
		--four: #ffd685;
		--three: #beb2c8;
		--dark: #101010;
	}
	.time {
		display: grid;
		grid-template-columns: 3fr 1fr;
		justify-items: center;
	}

	.six-percent::before {
		content: "6%";
		font-size: 5vw;
		font-style: italic;
		font-weight: 500;
		position: absolute;
		top: 0.4rem;
		right: 0.9rem;
		transition: all 1s;
	}
	.five-percent::before {
		content: "5%";
		font-size: 5vw;
		font-style: italic;
		font-weight: 500;
		position: absolute;
		top: 0.4rem;
		right: 0.9rem;
	}
	.four-percent::before {
		content: "4%";
		font-size: 5vw;
		font-style: italic;
		font-weight: 500;
		position: absolute;
		top: 0.4rem;
		right: 0.9rem;
	}
	.three-percent::before {
		content: "3%";
		font-size: 5vw;
		font-style: italic;
		font-weight: 500;
		position: absolute;
		top: 0.4rem;
		right: 0.9rem;
	}
	.six-percent {
		background: linear-gradient(70deg, transparent, #ffadd2);
	}
	.five-percent {
		background: linear-gradient(70deg, transparent, #b2faf5);
	}
	.four-percent {
		background: linear-gradient(70deg, transparent, #ffd685);
	}
	.three-percent {
		background: linear-gradient(70deg, transparent, #beb2c8);
	}
	.bonus {
		border-radius: 3px;
		padding: 1rem;
		margin: 0.5rem 0.2rem;
		position: relative;
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
		padding: 0.1rem 2rem;
		transform: translateY(1.8rem);
	}
</style>
