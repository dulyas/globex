<script lang="ts">
	import SeachIcon from "../icons/SeachIcon.svelte";
	import { getContext } from "svelte";
	import type { Writable } from "svelte/store";

	const queryString: Writable<string> = getContext("queryString");
	const loading: Writable<boolean> = getContext("loading");

	let debouce = false;
	let timeout;

	const onChange = (e: Event) => {
		$loading = true;
		clearTimeout(timeout);
		debouce = true;
		timeout = setTimeout(() => {
			console.log("onChange2");
			$queryString = (e.target as HTMLInputElement).value;
		}, 2000);
	};
</script>

<div class="search">
	<input on:input={onChange} type="text" />
	<SeachIcon />
</div>

<style lang="scss">
	.search {
		width: 100%;
		display: flex;
		justify-content: center;
		align-items: center;
		border-radius: 24px;
		padding: 12px 24px;
		border: 1px solid var(--blueberry, #d4defe);
		input {
			width: 100%;
			border: none;
			&:focus {
				border: none;
				outline: none;
			}
		}
	}
</style>
