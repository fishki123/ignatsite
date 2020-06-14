<script>
	import { createEventDispatcher } from 'svelte';
	import { goto, stores } from '@sapper/app';
	const { page, session } = stores();
	import { post } from 'utils.js';
	export let inProgress, image, username, bio, email = '';
	const dispatch = createEventDispatcher();

	function submit(event) {
		dispatch('save', { image, username, bio, email});
	}
</script>

<form on:submit|preventDefault='{submit}'>
	<fieldset>
		<fieldset class="form-group">
			<input class="form-control" type="text" placeholder="URL картинка для иконки" bind:value={image}>
		</fieldset>

		<fieldset class="form-group">
			<input class="form-control form-control-lg" type="text" placeholder="Логин" bind:value={username}>
		</fieldset>

		<fieldset class="form-group">
			<textarea class="form-control form-control-lg" rows="8" placeholder="Биография о вас" bind:value={bio}/>
		</fieldset>

		<fieldset class="form-group">
			<input class="form-control form-control-lg" type="email" placeholder="Почта" bind:value={email}>
		</fieldset>

		<button class="btn btn-lg btn-primary pull-xs-right" type="submit" disabled={inProgress}>
			Обновить настройки
		</button>

		<button class="btn btn-lg btn-primary pull-xs-left" type="submit">
			<a class="h3-norm" href='/profile/@{$session.user.username}/favorites'>Вернуться в профиль</a>
		</button>
	</fieldset>
</form>