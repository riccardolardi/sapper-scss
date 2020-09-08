<script>
	import { onMount, setContext } from 'svelte';
	import { writable } from 'svelte/store';
	import { getBrowserLocales } from '../functions.js';
	import Nav from '../components/Nav.svelte';
	export let segment;
	let data = writable(undefined);
	let lang = writable(getBrowserLocales({languageCodeOnly: true})[0] === 'de' ? 0 : 1);
	let seg = writable(segment);
	setContext('data', data);
	setContext('lang', lang);
	setContext('seg', seg);
	onMount(async () => {
		const res = await fetch(`/data.json`);
		$data = await res.json();
	});
</script>

<style type="text/scss" global>
	@import "../style/var.scss";
	@import "../style/type.scss";
	@import "../style/block.scss";
	@import "../style/_layout.scss";
</style>

{#if $data}
<main class="_layout font-main {!segment ? 'is-intro' : null}">
	<Nav {segment} />
	<slot />
</main>
{/if}