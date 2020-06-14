<script>
	import { onMount } from 'svelte';
	import MainView from './MainView/index.svelte';
	import Tags from './Tags.svelte';
	import * as api from 'api.js';

	export let p = 1;

	let tab;
	let tag;
	let tags;

	function setTags({ detail }) {
		tag = detail.tag;
		tab = "tag";
	}

	onMount(async () => {
		({ tags } = await api.get('tags'));
	});
</script>

<svelte:head>
	<title>Главное меню Ignat Japan</title>
</svelte:head>

<div class="home-page">
	<div class="banner">
		<div class="container">
			<p><img  class="ignatimage" src="https://i.ibb.co/1n212y8/Ignat-Japan.jpg" alt="Ignat-Japan" border="0"></p>
		</div>
	</div>
	<div class="container page">
		<div class="maintext">
			<p> Ignat Japan - это ( в значительной степени ) академический сайт, посвященный различным аспектам одной из великих мировых литератур.
				Сайт имеет тенденцию расширяться неторопливо, тем не менее, здесь есть материал, который возможно недоступен в других местах, поэтому не стесняйтесь просматривать.</p>
			<p class="maintext2">Японская литература — литература на японском языке, хронологически охватывающая период почти в полтора тысячелетия: от летописи «Кодзики» (712 год) до произведений современных авторов.
				На ранней стадии своего развития испытала сильнейшее влияние китайской литературы и зачастую писалась на классическом китайском. Влияние китайского в разной степени ощущалось вплоть до конца периода
				Эдо, сведясь к минимуму в XIX веке, начиная с которого развитие японской литературы стало во многом обусловлено продолжающимся до настоящего времени диалогом с европейской литературой.</p>
		</div>
	</div>
</div>