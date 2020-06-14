<script>
	import * as api from 'api.js';

	export let article;
	export let user;

	async function toggleFavorite() {
		// optimistic UI
		if (article.favorited) {
			article.favoritesCount -= 1;
			article.favorited = false;
		} else {
			article.favoritesCount += 1;
			article.favorited = true;
		}

		({ article } = await (article.favorited
				? api.post(`articles/${article.slug}/favorite`, null, user && user.token)
				: api.del(`articles/${article.slug}/favorite`, user && user.token)));
	}
	import Rate from "../ArticleList/Rate.svelte";

	const beforeRate = rate => {
		console.log(rate);
	};
	const afterRate = rate => {
		console.log(rate);
	};
</script>

<div class="article-preview">
	<div class="article-meta">
		<div class="info">
			<span class="date">
				{new Date(article.createdAt).toDateString()}
			</span>
		</div>

		{#if user}
			<div class="pull-xs-right">
				<button class='btn btn-sm {article.favorited ? "btn-primary" : "btn-outline-primary"}' on:click={toggleFavorite}>
					<i class="ion-plus-round"></i>
					{article.favoritesCount ? 'Убрать из списка' : 'Добавить в список'}
				</button>
			</div>
		{/if}
	</div>
	<a href='/article/{article.slug}' rel='prefetch' class="preview-link">
		<div class="six">
			<div class="three container">
				<div class="ten">
					<div class="five"></div>
				</div>
				<div class="ten">
					<div class="four">
						<div class="seven" style="text-align: center">
							<h2>{article.title}</h2>
							<div class="teg">
								{#each article.tagList as tag}
									<li class="tag-default tag-pill tag-outline">
										{tag}
									</li>
								{/each}
							</div>
						</div>
						<div class="nine">
							<p class="leading-normal text-left slide-in-bottom-subtitle">
								{article.description}
							</p>
						</div>
					</div>
				</div>
			</div>
		</div>
	</a>
</div>
<style>
	.awe
	{
	}
	.teg
	{
		margin-bottom: 10px;
	}
	.three
	{
		flex-1: auto;
		background-color: #e2e8f0;
		box-shadow: 2px 2px 8px rgba(0,0,0,0.1);
		border: black;
		border-radius: 2px;
		border: 1px solid #aaa;
		padding: 4px;
	}
	.four
	{
		background-color: #f7fafc;
		padding:20px;
		border: 1px solid #000;
		border-radius: 4px;
		font-family: 'Roboto', sans-serif;
	}
	.five
	{
		background-color: #718096;
		width: auto;
		height: 256px;
		border: 1px solid #000;
		border-radius: 4px;
		font-family: 'Roboto', sans-serif;
	}
	.six
	{
		padding: 4px;
	}
	.seven
	{
		width: auto;
		height: auto;
		color: blue;
		font-weight: bold;
		align-items: center;
		font-family: 'Roboto', sans-serif;
	}
	.seven h2
	{
		color: blue;
	}
	.eight
	{
		font-weight: bold;
		font-family: 'Roboto', sans-serif;
	}
	.nine
	{
		font-family: 'Roboto', sans-serif;
	}
	.ten
	{
		padding:20px;
	}
</style>
