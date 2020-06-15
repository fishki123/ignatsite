<script>
	import { goto, stores } from '@sapper/app';
	import ListErrors from '../_components/ListErrors.svelte';
	import { post } from 'utils.js';

	const { session } = stores();

	let username='';
	let email = '';
	let password = '';
	let errors = null;

	async function submit(event) {
		const response = await post(`auth/login`, { email, password });

		// TODO handle network errors
		errors = response.errors;

		if (response.user) {
			$session.user = response.user;
			goto('/');
		}
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

<svelte:head>
	<title>Авторизация Ignat Japan</title>
</svelte:head>

<div class="auth-page">
	<div class="container page">
		<div class="row">
			<div class="col-md-6 offset-md-3 col-xs-12">
				<h1 class="text-xs-center h1-norm">Авторизация</h1>
				<p class="text-xs-center">
					<a href="/register">Нужен аккаунт?</a>
				</p>

				<ListErrors {errors}/>

				<form on:submit|preventDefault={submit}>
					<h3>
						<i class="ion-email ion"></i>
						Почта:
					</h3>
					<fieldset class="form-group">
						<input class="form-control form-control-lg" type="text" placeholder="" bind:value={email}>
					</fieldset>
					<h3>
						<i class="ion-key ion"></i>
						Пароль:
					</h3>
					<fieldset class="form-group">
						<input class="form-control form-control-lg" type="password" placeholder="" bind:value={password}>
					</fieldset>
					<button class="btn btn-lg btn-primary pull-xs-right" type="submit" disabled='{!email || !password}'>
						Авторизоваться
					</button>
				</form>
			</div>
		</div>
	</div>
</div>