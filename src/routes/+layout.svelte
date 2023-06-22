<script lang="ts">
	import '@fortawesome/fontawesome-free/css/all.css';
	import '@picocss/pico';
	import '../app.css';
	import Icon from '@iconify/svelte';
	import { onMount } from 'svelte';

	let isScrollAtTop: boolean = false;
	let themeName: null | 'dark' | 'light' = null;

	onMount(() => {
		const savedTheme = window.localStorage.getItem('theme');
		const htmlClass = document.documentElement.classList;

		if (!savedTheme || savedTheme === 'dark') {
			localStorage.setItem('theme', 'dark');
			htmlClass.add('dark');
			themeName = 'dark';
		} else {
			localStorage.setItem('theme', 'light');
			htmlClass.remove('dark');
			themeName = 'light';
		}
		function handleScroll() {
			const scrollTop = window.pageYOffset || document.documentElement.scrollTop;
			isScrollAtTop = scrollTop >= 1 ? true : false;
		}

		window.addEventListener('scroll', handleScroll);

		return () => {
			window.removeEventListener('scroll', handleScroll);
		};
	});

	function handleClick() {
		const savedTheme = window.localStorage.getItem('theme');
		const htmlClass = document.documentElement.classList;

		if (savedTheme === 'light') {
			localStorage.setItem('theme', 'dark');
			htmlClass.add('dark');
			themeName = 'dark';
		} else {
			localStorage.setItem('theme', 'light');
			htmlClass.remove('dark');
			themeName = 'light';
		}
	}
</script>

<div class="w-full h-full fixed top-0 z-0" />
<nav
	class={`px-3 text-black dark:text-white sticky z-20 top-0 py-4 ${
		isScrollAtTop ? 'bg-slate-200 dark:bg-slate-900' : 'bg-transparent'
	}`}
>
	<div class="flex items-center justify-between w-full xl:container mx-auto">
		<a href="/" class="font-bold text-sm" title="home">First-Contribution-</a>
		<div>
			<button
				type="button"
				title={themeName === 'dark' ? 'Toggle to light theme' : 'Toggle to dark theme'}
				on:click={handleClick}
				class="w-fit text-sm px-2 rounded-full bg-slate-200 dark:bg-slate-900 flex items-center justify-center gap-2 capitalize border-2 border-transparent hover:border-white dark:hover:border-black shadow-lg shadow-slate-500/20 hover:shadow-slate-500/40"
			>
				{themeName}
				{#if themeName === 'dark'}
					<Icon icon="solar:moon-bold" />
				{:else}
					<Icon icon="solar:sun-bold" />
				{/if}
			</button>
		</div>
	</div>
</nav>
<header class="relative xl:container mx-auto flex flex-col items-center py-20 px-3">
	<h1 class="text-center text-2xl md:text-3xl font-extrabold text-black dark:text-white">
		Contribute to Open Source 🚀
	</h1>
	<p class="text-center py-2 font-light text-gray-500 max-w-[1000px]">
		Get started in Open Source with our beginner-friendly repo. Add your GitHub profile name and
		make your first contribution. Join a supportive community and launch your journey as an Open
		Source contributor.
	</p>
	<a
		href="https://github.com/Raulj123/First-Contribution-"
		target="_blank"
		rel="noopener noreferrer"
		title="contribute to first-contribution"
		class="py-1 px-3 rounded-lg mt-5 bg-slate-200 dark:bg-slate-900 border-2 border-transparent hover:border-white dark:hover:border-black shadow-lg shadow-slate-500/20 hover:shadow-slate-500/40 flex items-center gap-2"
		>Contribute Now
		<Icon icon="bi:github" />
	</a>
</header>
<main class="relative">
	<slot />
</main>

<footer class="py-5 text-center">
	Made with <span class="animate-pulse">💖</span> by Raul Jarquin
</footer>
