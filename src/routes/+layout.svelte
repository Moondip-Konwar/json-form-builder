<script lang="ts">
	import "./layout.css";
	import favicon from "$lib/assets/favicon.svg";
	import { FileBraces, Menu } from "lucide-svelte";
	import { resolve } from "$app/paths";

	let { children } = $props();
</script>

<svelte:head><link rel="icon" href={favicon} /></svelte:head>

<!-- Navbar -->
<nav
	class="flex flex-row px-8 py-4 border-gray-300 border-b-2 justify-between items-stretch"
>
	<!-- Title  -->
	<a class="flex flex-row items-center gap-4" href={resolve("/")}>
		<FileBraces size="24" strokeWidth="1.3"></FileBraces>
		<span class="text-xl">Json Forms</span>
	</a>

	<!-- Links -->
	<div class="flex flex-row gap-4 items-center" id="nav-links">
		<a href={resolve("/new")}>New</a>
		<a href="/">Github</a>
		<a href={resolve("/") + "#about"}>About</a>
	</div>
</nav>

<!-- Body -->
{@render children()}

<!-- Footer -->
<footer
	class="mt-auto flex flex-col gap-6 px-8 py-10 border-t-2 border-gray-300"
>
	<div
		class="flex flex-col md:flex-row justify-between items-start md:items-center gap-6"
	>
		<div class="flex flex-col gap-2">
			<div class="flex items-center gap-2">
				<FileBraces size="20" strokeWidth="1.5" />
				<span class="font-bold text-lg">Json Forms</span>
			</div>
			<p class="text-sm text-gray-500">
				Building structured data, one field at a time.
			</p>
		</div>

		<div class="grid grid-cols-2 sm:grid-cols-3 gap-8">
			<div class="flex flex-col gap-2">
				<span class="text-xs uppercase tracking-widest text-gray-800 font-bold"
					>Product</span
				>
				<a href={resolve("/new")}>Builder</a>
				<a href="/">Templates</a>
			</div>
			<div class="flex flex-col gap-2">
				<span class="text-xs uppercase tracking-widest text-gray-800 font-bold"
					>Resources</span
				>
				<a href="/">Docs</a>
				<a href="/">Github</a>
			</div>
		</div>
	</div>

	<div
		class="pt-6 border-t border-gray-100 flex justify-between items-center text-xs text-gray-800"
	>
		<p>© {new Date().getFullYear()} SomeUselessPerson.</p>
		<p>Built with Svelte 5</p>
	</div>
</footer>

<!-- Style -->
<style>
	footer a {
		color: var(--color-gray-500);
	}
	a {
		text-decoration: none;
		color: black;
		font-weight: 500;
	}

	a:hover {
		box-shadow:
			0 1px 0 0 currentColor,
			0 1px 0 0 currentColor,
			0 1px 0 0 currentColor;
	}
</style>
