<script>
	import { getContext } from 'svelte';
	export let segment;
	const data = getContext('data');
	const lang = getContext('lang');
	$: slugs = $data.nav.map(el => el[1].toLowerCase());
</script>

<style type="text/scss">
	@import "../style/var.scss";
	@import "../style/nav.scss";
</style>

<nav class="{!segment ? 'is-intro' : null}">
	<ul class="nav-items">
		{#each $data.nav as navItem, index}
		<li class="{segment === slugs[index] ? 'active' : null}">
			<a aria-current="{segment === slugs[index] ? 'page' : null}" href="/{slugs[index]}">
				{navItem[$lang]}
			</a>
		</li>
		{/each}
	</ul>
	<ul class="lang-select">
		<li><button>DE</button></li>
		<li><button>EN</button></li>
	</ul>
</nav>