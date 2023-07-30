<script lang="ts">
	import { getContext } from "svelte";
	import Card from "./Card.svelte";
	import type { ICard } from "../types/ICard";
	import type { Writable } from "svelte/store";

	let cards: ICard[] = [];

	const queryString: Writable<string> = getContext("queryString");
	const loading: Writable<boolean> = getContext("loading");
	const apiUrl = "http://localhost:3000/";

	$: getData($queryString);

	const getData = async (queryString: string) => {
		$loading = true;
		try {
			const generateQuery = (queryString) => {
				if (!queryString) return apiUrl;
				return apiUrl + "?" + "term=" + queryString;
			};

			const res = await fetch(generateQuery(queryString));
			cards = await res.json();
		} catch (error) {
			console.log(error);
			cards = [];
		}
		$loading = false;
	};
</script>

<div class="cards">
	{#if $loading}
		Loading...
	{:else if cards.length}
		{#each cards as card (card.email)}
			<Card {card} />
		{/each}
	{:else}
		No Cards for this params
	{/if}
</div>

<style lang="scss">
	.cards {
		margin-block-start: 32px;

		display: flex;
		justify-content: center;
		align-items: center;
		flex-wrap: wrap;
		gap: 25px;
	}
</style>
