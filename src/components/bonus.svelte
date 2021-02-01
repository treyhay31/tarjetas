<script>
	export let cardName;
	export let bonuses;
	export let url;
</script>

<section>
	<h2>
		<a href={url}>{cardName} Bonuses</a>
	</h2>
	<ul>
		{#each bonuses as bonus, i}
			<li>
				{bonus}
			</li>
		{/each}
	</ul>
</section>