<script context="module">
	import * as api from 'api.js';

	export async function preload({ params }) {
		const { slug } = params;
		const { article } = await api.get(`articles/${params.slug}`, null);

		return { article, slug };
	}
</script>

<script>
	import { onMount } from 'svelte';
	import { stores } from '@sapper/app';
	import marked from 'marked';

	import ArticleMeta from './_ArticleMeta.svelte';
	import CommentContainer from './_CommentContainer.svelte';

	export let article;
	export let slug;

	const { session } = stores();

	let commentErrors, comments = []; // we'll lazy-load these in onMount
	$: markup = marked(article.body);

	onMount(() => {
		api.get(`articles/${slug}/comments`).then((res) => {
			comments = res.comments;
		});
	});
</script>

<svelte:head>
	<title>{article.title}</title>
</svelte:head>

<div class="article-page">
	<div class="banner">
		<div class="container">
			<div class="article-meta">
				<div class="info">
			<span class="date">
				<i class="ion-calendar ion"></i>
				{new Date(article.createdAt).toDateString()}
			</span>
				</div>
			</div>
			<div class="tens">
				<img src="{article.poster}" alt="pos">
			</div>
			<h1 class="we"style="text-align: center">{article.title}</h1>
			<ArticleMeta {article} user={$session.user}/>
		</div>
	</div>

	<div class="container page">
		<div class="row article-content">
			<div class="col-xs-12">

				<div class="desc">{@html markup}</div>

				<ul class="tag-list we">
					{#each article.tagList as tag}
						<li class="tag-default tag-pill tag-outline">
							{tag}
						</li>
					{/each}
				</ul>
			</div>
		</div>
		<hr />
		<div class="article-actions"></div>
		<div class="row">
			<CommentContainer {slug} {comments} user={$session.user} errors={commentErrors}/>
		</div>
	</div>
</div>
<style>
	.tens
	{
		border: 4px;
		border-color: black;
		align-items: center;
		text-align: center;
	}
	.we
	{
		margin-top: 30px;
	}
	.desc
	{
		padding: 1.25rem;
		background-color: #f7fafc;
		border: 4px;
		border-color: black;
		height: auto;
		box-shadow: 2px 2px 8px rgba(0,0,0,0.1);
		border-radius: 4px;
		border: 1px solid #000;
		font-family: 'Roboto', sans-serif;
		width: 100%;
	}
</style>