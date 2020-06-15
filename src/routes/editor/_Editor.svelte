<script>
	import { goto, stores } from '@sapper/app';
	import ListErrors from '../_components/ListErrors.svelte';
	import * as api from 'api.js';

	export let article;
	export let slug;

	let inProgress = false;
	let errors;

	const { session } = stores();

	function addTag(input) {
		article.tagList = [...article.tagList, input.value];
		input.value = '';
	}

	function remove(index) {
		article.tagList = [...article.tagList.slice(0, index), ...article.tagList.slice(index + 1)];
	}

	async function publish() {
		inProgress = true;

		const response = await (slug
			? api.put(`articles/${slug}`, { article }, $session.user && $session.user.token)
			: api.post('articles', { article }, $session.user && $session.user.token));

		if (response.article) {
			goto(`/article/${response.article.slug}`);
		}

		inProgress = false;
	}

	function enter(node, callback) {
		function onkeydown(event) {
			if (event.which === 13) callback(node);
		}

		node.addEventListener('keydown', onkeydown);

		return {
			destroy() {
				node.removeEventListener('keydown', onkeydown);
			}
		};
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
</script>
<div class="editor-page">
	<div class="container page">
		<div class="row">
			<div class="col-md-10 offset-md-1 col-xs-12">
				<ListErrors {errors}/>

				<form>
					<fieldset>
						<fieldset class="form-group">
							<h3>
								<i class="ion-document ion"></i>
								Название:
							</h3>
							<input class="form-control form-control-lg" type="text" placeholder="" bind:value={article.title}>
						</fieldset>
							<h3>
								<i class="ion-document-text ion"></i>
								Краткое описание:
							</h3>
						<fieldset class="form-group">
							<input class="form-control" type="text" placeholder="" bind:value={article.description}>
						</fieldset>
							<h3>
								<i class="ion-clipboard ion"></i>
								Подробное описание:
							</h3>
						<fieldset class="form-group">
							<textarea class="form-control" rows="8" placeholder="" bind:value={article.body}/>
						</fieldset>
							<h3>
								<i class="ion-pricetags ion"></i>
								Теги
								/
								<i class="ion-wand ion"></i>
								жанры:
							</h3>
						<fieldset class="form-group">
							<input class="form-control" type="text" placeholder="" use:enter={addTag}>

							<div class="tag-list">
								{#each article.tagList as tag, i}
									<span class="tag-default tag-pill">
										<i class="ion-close-round" on:click='{() => remove(i)}'/>
										{tag}
									</span>
								{/each}
							</div>
						</fieldset>
						<button class="btn btn-lg pull-xs-right btn-primary" type="button" disabled={inProgress} on:click={publish} on:click={sendPositive} status="positive">
							Опубликовать литературу
						</button>
						<Notifications />
					</fieldset>
				</form>
			</div>
		</div>
	</div>
</div>
<style>
	.ion
	{
		color:black;
	}
</style>