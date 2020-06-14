<script>
    import { stores } from '@sapper/app';
    import { onMount } from 'svelte';
    import MainView from '../_components/MainView/index.svelte';
    import Tags from '../_components/Tags.svelte';
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
    const { page, session } = stores();
    import Button from "svelte-atoms/Button.svelte";
    import Notifications, { sendNotification } from "svelte-atoms/Notifications.svelte";

    const sendSimple = () => sendNotification("Simple notification");

    const sendNegative = () => sendNotification("Negative notification", { status: "negative" });

    const sendPositive = () => sendNotification("Positive notification with custom icon", {
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
    <title>Японская литература</title>
</svelte:head>
<div class="first">
    <div class="second" id="myDropdown">
        {#if $session.user}
        <div class="container page">
            <a rel='' href="/editor" class:active="{$page.path === '/editor'}" >
                <i class="ion-compose">Добавить японскую литературу</i>&nbsp;
            </a>
        </div>
            <MainView  {p} {tag} bind:tab />
        {:else}
            <MainView {p} {tag} bind:tab />
        {/if}
    </div>
</div>