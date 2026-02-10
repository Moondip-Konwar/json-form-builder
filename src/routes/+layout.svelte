<script lang="ts">
	import "./layout.css";
	import favicon from "$lib/assets/favicon.svg";
	import { FileBraces, Menu } from "lucide-svelte";

	let { children } = $props();
</script>

<svelte:head><link rel="icon" href={favicon} /></svelte:head>

<!-- Navbar -->
<nav
	class="fixed w-screen flex flex-row px-8 py-4 border-gray-300 border-b-2 justify-between items-stretch"
>
	<!-- Title  -->
	<div class="flex flex-row items-center gap-4">
		<FileBraces size="24" strokeWidth="1.3"></FileBraces>
		<span class="text-xl">Json Forms</span>
	</div>

	<!-- Links -->
	<div class="flex flex-row gap-4 items-center" id="nav-links">
		<a href="/">Github</a>
		<a href="/">About</a>
	</div>
</nav>

<!-- Body -->
{@render children()}

<!-- Style -->
<style>
	#nav-links > a {
		text-decoration: none;
		color: black;
		font-weight: 500;
	}

	#nav-links > a:hover {
		box-shadow:
			0 1px 0 0 currentColor,
			0 1px 0 0 currentColor,
			0 1px 0 0 currentColor;
	}
</style>
