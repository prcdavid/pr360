<script>
	// @ts-nocheck

	import '$css/app.css';
	import { onMount } from 'svelte';

	let root;
	let scheme;
	let prop;

	function setColorScheme(userScheme) {
		if (!root) return;

		root.setAttribute('color-scheme', userScheme);
		root.dataset.theme = userScheme;

		console.log('Set Color Scheme to ' + userScheme);
	}

	$: setColorScheme(scheme);

	function cycle() {
		if (scheme === 'light') scheme = 'hybrid';
		else if (scheme === 'hybrid') scheme = 'dark';
		else if (scheme === 'dark') scheme = 'light';
		console.log('Swap Color Scheme');
	}

	onMount(() => {
		root = document.documentElement;
		scheme = 'hybrid'; // get this from the store
	});
</script>

<div on:click={() => cycle()} class="themeCheck">
	<div>Text</div>
</div>
<slot />

<style lang="scss">
	@use '../scss/theme';
	@include theme.default(true);

	.themeCheck {
		display: inline-flex;
		align-items: center;
		justify-content: center;
		width: 200px;
		height: 200px;
		font-size: 32px;
		border-radius: 6px;
		border-color: var(--colors-border);
		border-style: solid;
		border-width: 3px;
		background-color: var(--colors-background);
		color: var(--colors-text);
		cursor: pointer;
		user-select: none;
	}
</style>
