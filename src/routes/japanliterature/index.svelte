<script>
    import { goto, stores } from '@sapper/app';
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
    import { createEventDispatcher } from 'svelte';
    export let filters;
    export let filtered;
    const dispatch = createEventDispatcher();
    let selected = filtered ? filtered : 'all';
    function updateFilter(event) {
        if (selected) {
            dispatch('updatefilter', selected);
        }
    }
    if (typeof window !== 'undefined') {
        // If the user uses the forward or backward button - set the select box and content
        window.onpopstate = function(event) {
            const urlParams = new URLSearchParams(window.location.search);

            // Get the parameter from the URL and update selected
            selected = urlParams.has('filter') ? urlParams.get('filter') : 'all';
            // Update the content
            dispatch('updatefilter', selected);
        }
    }
</script>
<svelte:head>
    <title>Японская литература</title>
</svelte:head>
<div class="first">
    <div class="second">
        {#if $session.user}
        <div class="container page">
            <a rel='' href="/editor" class:active="{$page.path === '/editor'}" >
                <i class="ion-compose"></i>&nbsp;
                Добавить японскую литературу
            </a>
        </div>
        <div class="row">
            <MainView {p} {tag} bind:tab />
        </div>
        {:else}
            <div class="row">
                <MainView {p} {tag} bind:tab />
            </div>
        {/if}
    </div>
</div>