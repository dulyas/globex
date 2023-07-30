<script lang="ts">
	import Search from "./components/Search.svelte";
	import Cards from "./components/Cards.svelte";
	import Modal from "./components/Modal.svelte";
	import { writable } from "svelte/store";
	import { setContext } from "svelte";
	import type { ICard } from "./types/ICard";

	const modalCard = writable<ICard | null>(null);
	const loading = writable<boolean>(false);
	const queryString = writable<string>("");

	setContext("modalCard", modalCard);
	setContext("loading", loading);
	setContext("queryString", queryString);
</script>

<div
	style="--blueberry: #D4DEFE; --purplefog: #432EAB; --plumbum: #262C40; --background-light-stroke: rgba(188, 195, 208, 0.50); --asphalt: #8189A3;"
	class="app"
>
	{#if $modalCard}
		<Modal />
	{/if}
	<div class="wrap">
		<div class="search">
			<Search />
		</div>
		<Cards />
	</div>
</div>

<style lang="scss">
	.app {
		width: 100%;
		height: 100%;
		position: absolute;
		.wrap {
			width: 100%;
			padding: 60px 80px 0;
			@media (max-width: 532px) {
				padding: 30px 40px 0;
			}
		}
	}
</style>
