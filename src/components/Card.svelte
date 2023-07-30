<script lang="ts">
	import type { ICard } from "../types/ICard";
	import MailIcon from "../icons/MailIcon.svelte";
	import PhoneIcon from "../icons/PhoneIcon.svelte";
	import { getContext, type SvelteComponent } from "svelte";
	import type { Writable } from "svelte/store";

	export let card: ICard;

	const modalCard: Writable<ICard | null> = getContext("modalCard");

	type IRows = {
		Icon: typeof SvelteComponent;
		title: string;
	};

	const rows: IRows[] = [
		{
			Icon: PhoneIcon as typeof SvelteComponent,
			title: card.phone,
		},
		{
			Icon: MailIcon as typeof SvelteComponent,
			title: card.email,
		},
	];
</script>

<button on:click={() => ($modalCard = card)} class="card">
	<div class="name">
		{card.name}
	</div>
	<div class="opts">
		{#each rows as { Icon, title }}
			<div class="row">
				<Icon />
				<span>
					{title}
				</span>
			</div>
		{/each}
	</div>
</button>

<style lang="scss">
	.card {
		min-width: 357px;
		flex-grow: 0;
		flex-shrink: 1;
		width: calc(33% - 12.8px);
		height: 314px;
		padding: 24px;
		border-radius: 16px;
		background: #fff;
		box-shadow: 0px 0px 20px 0px rgba(0, 0, 0, 0.1);
		cursor: pointer;
		@media (max-width: 532px) {
			min-width: calc(100% - 30px);
			width: 100%;
		}
		.name {
			color: var(--plumbum);
			font-size: 24px;
		}
		.opts {
			margin-block-start: 24px;
			.row {
				display: flex;
				align-items: center;
				span {
					margin-inline-start: 14px;
				}
				&:not(&:first-child) {
					margin-block-start: 12px;
				}
			}
		}
	}
</style>
