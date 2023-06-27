<script lang="ts">
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
				class="w-fit text-sm px-2 rounded-full bg-slate-200 dark:bg-slate-900 flex items-center justify-center gap-2 capitalize border-2 border-transparent hover:border-white dark:hover:border-black shadow-lg shadow-slate-500/20 hover:shadow-slate-500/40 focus:ring-2"
			>
				{#if themeName === 'dark'}
					light
					<Icon icon="solar:sun-bold" />
				{:else}
					dark
					<Icon icon="solar:moon-bold" />
				{/if}
			</button>
		</div>
	</div>
</nav>
