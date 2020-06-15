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
				<i class="ion-calendar ion"></i>
				{new Date(article.createdAt).toDateString()}
			</span>
		</div>
	</div>
	<a href='/article/{article.slug}' rel='prefetch' class="preview-link">
		<div class="six">
			<div class="three container">
				<div class="tens">
					<img src="{article.poster}" alt="post">
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
	.tens
	{
		align-items: center;
		text-align: center;
		width: auto;
		height:auto;
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
	.nine
	{
		font-family: 'Roboto', sans-serif;
	}
	.ten
	{
		padding:20px;
	}
</style>
