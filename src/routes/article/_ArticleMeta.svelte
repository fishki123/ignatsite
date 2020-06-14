<script>
	import { goto } from '@sapper/app';
	import * as api from 'api.js';

	export let article;
	export let user;

	$: canModify = user && article.author.username === user.username;

	async function remove() {
		await api.del(`articles/${article.slug}`, user && user.token);
		goto('japanliterature');
	}
	import Notifications, { sendNotification } from "svelte-atoms/Notifications.svelte";

	const sendSimple = () => sendNotification("Simple notification");

	const sendNegative = () => sendNotification("Negative notification", { status: "negative" });

	const sendPositive = () => sendNotification("Успешно!", {
		status: "positive",
		icon: "check",
	});
	const sendPrimary = () => sendNotification("Primary with cusom delay", {
		status: "primary",
		delay: 10000
	});

	const sendWarning = () => sendNotification("Warning with no icon", {
		status: "warning",
		noIcon: true
	});

	import Rate from "../_components/ArticleList/Rate.svelte";

	const beforeRate = rate => {
		console.log(rate);
	};
	const afterRate = rate => {
		console.log(rate);
	};
</script>

<div class="article-meta">
	{#if canModify}
			<div class="dropdown sf">
				<a rel='prefetch' role="button" aria-pressed="true" href="/" style="text-align: center" aria-haspopup="true" aria-expanded="false" data-toggle="dropdown" class="nav-dropdown_2 dropdown-menu-right_2">
					Список функции
				</a>
				<div class="nav-dropdown_2 dropdown-menu dropdown-menu-right_2" style="text-align: center">
					<span>
						<a href='/editor/{article.slug}' class="btn btn-outline-secondary btn-sm">
							<i class="ion-edit"/> Редактировать
						</a>
						<button class="btn btn-outline-danger btn-sm" on:click='{remove}' on:click={sendPositive} status="positive">
							<i class="ion-trash-a"/> Удалить литературу
						</button>
						<Notifications />
					</span>
				</div>
			</div>
	{/if}
</div>