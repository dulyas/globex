<script lang="ts">
	import { getContext } from "svelte";
	import type { Writable } from "svelte/store";
	import { fade } from "svelte/transition";
	import type { ICard } from "../types/ICard";
	import ExitIcon from "../icons/ExitIcon.svelte";

	const modalCard: Writable<ICard | null> = getContext("modalCard");

	const { name, phone, email, hire_date, position_name, department } =
		$modalCard;

	type IRow = {
		title: string;
		content: string;
	};

	const rows: IRow[] = [
		{
			title: "Телефон",
			content: phone,
		},
		{
			title: "Почта",
			content: email,
		},
		{
			title: "Дата Приема",
			content: hire_date,
		},
		{
			title: "Должность",
			content: position_name,
		},
		{
			title: "Подразделение",
			content: department,
		},
	];

	const closeModal = () => ($modalCard = null);
</script>

<!-- svelte-ignore a11y-click-events-have-key-events -->
<!-- svelte-ignore a11y-no-static-element-interactions -->
<div on:click|self={closeModal} transition:fade|local class="modal">
	<div class="content">
		<div class="name">{name}</div>
		<div on:click={closeModal} class="exit">
			<ExitIcon />
		</div>
		<div class="rows">
			{#each rows as { title, content }}
				<div class="row">
					<div class="title">{title}:</div>
					<div class="value">{content}</div>
				</div>
			{/each}
		</div>
		<div class="more-info">
			<div class="title">Дополнительная информация:</div>
			<div class="value">
				Разработчики используют текст в качестве заполнителя макта
				страницы. Разработчики используют текст в качестве заполнителя
				макта страницы.
			</div>
		</div>
	</div>
</div>

<style lang="scss">
	.modal {
		position: fixed;
		width: 100%;
		height: 100%;
		background: var(--background-light-stroke);
		z-index: 2;
		display: flex;
		justify-content: center;
		align-items: center;
		.content {
			border-radius: 16px;
			background: #fff;
			box-shadow: 0px 0px 20px 0px rgba(0, 0, 0, 0.1);
			position: relative;
			padding: 24px 24px 56px;
			color: var(--plumbum, #262c40);
			width: 90%;
			max-width: 500px;
			.title {
				font-size: 18px;
				font-weight: 400;
			}
			.value {
				color: var(--asphalt, #8189a3);
				font-size: 16px;
			}
			.exit {
				position: absolute;
				right: 24px;
				top: 24px;
				cursor: pointer;
			}
			.name {
				font-size: 24px;
				font-weight: 700;
			}
			.rows {
				margin-block-start: 40px;
				.row {
					display: flex;

					&:not(&:first-child) {
						margin-block-start: 14px;
					}
					.title {
						width: 30%;
						word-break: break-all;
					}
					.value {
						margin-inline-start: 40px;
						width: calc(70% - 40px);
					}
				}
			}
			.more-info {
				margin-block-start: 52px;
				.value {
					margin-block-start: 12px;
				}
			}
		}
	}
</style>
