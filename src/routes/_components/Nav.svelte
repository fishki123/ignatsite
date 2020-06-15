<script>
	import { goto, stores } from '@sapper/app';

	const { page, session } = stores();
	import { post } from 'utils.js';
	async function logout() {
		await post(`auth/logout`);
		$session.user = null;
		goto('/');
	}
</script>
<nav class="navbar navbar-light">
	<div class="container">
		<a rel='prefetch' class="navbar-brand nav-link" class:active="{$page.path === '/'}" href="/">Ignat Japan</a>
		<ul class="nav navbar-nav pull-xs-right">
			<li class="nav-item">
				<a rel='prefetch' class="nav-link" class:active="{$page.path === '/'}" href="/">
					<i class="ion-search"></i>
					<input>
				</a>
			</li>
			<li class="nav-item">
				<a rel='prefetch' class="nav-link" class:active="{$page.path === '/'}" href="/">
					<i class="ion-home"></i>
					Главное меню
				</a>
			</li>
			<li class="nav-item">
				<a rel='prefetch' class="nav-link" class:active="{$page.path === '/japanliterature'}" href="/japanliterature">
					<i class="ion-ios-book"></i>
					Японская литература
				</a>
			</li>
			{#if $session.user}
				<li class="nav-item">
					<div class="dropdown show">
						<a rel='prefetch' role="button" aria-pressed="true" href='/profile/@{$session.user.username}' style="text-align: center" aria-haspopup="true" aria-expanded="false" data-toggle="dropdown" class="nav-link ">
							{$session.user.username}
						</a>
						<div class="nav-dropdown dropdown-menu dropdown-menu-right" style="text-align: center">
							<a rel='prefetch' href='/profile/@{$session.user.username}/favorites' class="dropdown-item">
								<i class="ion-person"></i>
								Мой профиль
							</a>
							<a rel='prefetch' href='/admin' class="dropdown-item">
								<i class="ion-card"></i>
								Админ панель
							</a>
							<div class="dropdown-divider"></div>
							<button class="dropdown-item logout btn btn-outline-danger" on:click={logout}>
								<img src="https://img.icons8.com/ios-filled/50/000000/logout-rounded-up.png" alt="logout">
							</button>
						</div>
					</div>
				</li>
			{:else}
				<li class="nav-item">
					<a rel='prefetch' href="/login" class="nav-link" class:active="{$page.path === '/login'}">
						<i class="ion-log-in"></i>
						Авторизация
					</a>
				</li>

				<li class="nav-item">
					<a rel='prefetch' href="/register" class="nav-link" class:active="{$page.path === '/register'}">
						<i class="ion-document-text"></i>
						Регистрация
					</a>
				</li>
			{/if}
		</ul>
	</div>
</nav>
<style>
	@media (min-width: 544px)
	{
		.container
		{
			max-width: 576px;
		}
	}
	@media (min-width: 768px)
	{
		.container
		{
			max-width: 720px;
		}
	}
	@media (min-width: 992px)
	{
		.container
		{
			max-width: 940px;
		}
	}
	@media (min-width: 1200px)
	{
		.container
		{
			max-width: 1140px;
		}
	}
</style>