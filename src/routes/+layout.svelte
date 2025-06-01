<script lang="ts">
	import '../app.css';
	import { config } from '@fortawesome/fontawesome-svg-core';
	export const prerender = true;
	import '@fortawesome/fontawesome-svg-core/styles.css'; // <- penting untuk menghindari FOUC
	config.autoAddCss = false;

	let { children } = $props();
</script>

{@render children()}
