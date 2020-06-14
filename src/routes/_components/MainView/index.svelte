<script>
	import { stores } from '@sapper/app';
	import ArticleList from '../ArticleList/index.svelte';

	export let tab = 'all';
	export let tag = null;
	export let p;

	const { session } = stores();

	function yourFeed() {
		tab = "feed";
		tag = null;
	}

	function globalfeed() {
		tab = "all";
		tag = null;
	}
</script>

<div class="container page">
	<ArticleList {p} {tab} {tag}/>
</div>