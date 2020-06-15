<script>
	import { goto } from '@sapper/app';
	import ArticleList from '../../_components/ArticleList/index.svelte';
	import * as api from 'api.js';

	export let profile;
	export let favorites;
	export let user;

	$: isUser = user && (profile.username === user.username);

	async function toggleFollowing() {
		if (!user) return goto('/login');

		// optimistic UI
		profile.following = !profile.following;

		({ profile, favorites } = await (profile.following
			? api.post(`profiles/${profile.username}/follow`, null, user && user.token)
			: api.del(`profiles/${profile.username}/follow`, user && user.token)));
	}
	import Rate from "../../_components/ArticleList/Rate.svelte";

	const beforeRate = rate => {
		console.log(rate);
	};
	const afterRate = rate => {
		console.log(rate);
	};
</script>

<svelte:head>
	<title>{profile.username} Ignat Japan</title>
</svelte:head>
<div class="profile-page">
	<div class="user-info">
		<div class="container">
			<div class="row">
				<div class="col-xs-12 col-md-10 offset-md-1">
					<img src={profile.image} class="user-img" alt={profile.username} />
					<h4>{profile.username}</h4>
					<p>{profile.bio}</p>
					{#if isUser}
						<a href="/settings" class="btn btn-sm btn-outline-secondary action-btn">
							<i class="ion-gear-a"></i>
							Настройки
						</a>
					{/if}
				</div>
			</div>
		</div>
	</div>
	<div class="container">
		<div class="row">
			<div class="col-xs-12 col-md-10 offset-md-1">
				<div class="articles-toggle">
					<ul class="nav nav-pills outline-active">
						<li class="nav-item">
							<a class="nav-link {favorites ? 'active' : ''}" href='/profile/@{profile.username}/favorites'>Список запланированных литератур</a>
						</li>
					</ul>
				</div>
				<ArticleList tab='profile' username='{profile.username}' {favorites}/>
			</div>
		</div>
	</div>
</div>