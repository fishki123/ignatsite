<script>
	import { goto, stores } from '@sapper/app';
	import ListErrors from '../_components/ListErrors.svelte';
	import { post } from 'utils.js';

	const { session } = stores();

	let username = '';
	let email = '';
	let password = '';

	let errors = null;

	async function submit(event) {
		const response = await post(`auth/register`, { username, email, password });

		// TODO handle network errors
		errors = response.errors;

		if (response.user) {
			$session.user = response.user;
			goto('/');
		}
	}
</script>

<svelte:head>
	<title>Регистрация Ignat Japan</title>
</svelte:head>

<div class="auth-page">
	<div class="container page">
		<div class="row">
			<div class="col-md-6 offset-md-3 col-xs-12">
				<h1 class="text-xs-center h1-norm">Регистрация</h1>
				<p class="text-xs-center">
					<a href="/login">Есть аккаунт?</a>
				</p>

				<ListErrors {errors}/>

				<form on:submit|preventDefault={submit}>
					<fieldset class="form-group">
						<input class="form-control form-control-lg" type="text" placeholder="Логин" bind:value={username}>
					</fieldset>
					<fieldset class="form-group">
						<input class="form-control form-control-lg" type="email" placeholder="Почта" bind:value={email}>
					</fieldset>
					<fieldset class="form-group">
						<input class="form-control form-control-lg" type="password" placeholder="Пароль" bind:value={password}>
					</fieldset>
					<fieldset class="form-group">
						<input class="form-control form-control-lg" type="text" placeholder="invite-код">
					</fieldset>
					<button class="btn btn-lg btn-primary pull-xs-right">
						Зарегистрироваться
					</button>
				</form>
			</div>
		</div>
	</div>
</div>