<script lang="ts">
	import { contributors } from './contributors';
	import Icon from '@iconify/svelte';
	let isList = true;

	function handleGrid() {
		isList ? (isList = false) : (isList = true);
	}
</script>

<section class="xl:container mx-auto">
	<header class=" flex justify-between items-center p-3">
		<h2 class="text-black dark:text-white font-medium">
			Total contributor <span class="text-sm">{contributors.length}</span>
		</h2>
		<button type="button" class="w-fit border-none" on:click={handleGrid}>
			{#if isList}
				<Icon icon="ri:grid-fill" />
			{:else}
				<Icon icon="fa-solid:list" />
			{/if}
		</button>
	</header>
	<hr class="border-slate-500/10" />

	<ul class={`grid ${!isList ? 'md:grid-cols-2' : 'grid-cols-1'}`}>
		{#each contributors as contributor}
			<li
				class="flex gap-3 p-3 hover:bg-slate-100 dark:hover:bg-slate-900 m-0 items-center group"
				title={contributor.name}
			>
				<figure class="shadow-lg shadow-transparent group-hover:shadow-slate-500 rounded-full">
					<img
						src={`https://avatars.githubusercontent.com/${contributor.github.split('/').at(-1)}`}
						alt="{contributor.name}'s Avatar"
						class="w-16 aspect-square object-cover rounded-full"
					/>
				</figure>
				<p class="w-full text-slate-800 dark:text-slate-200">
					{contributor.name}
					<span class="block text-xs opacity-50">@{contributor.github.split('/').at(-1)}</span>
				</p>
				<a
					href={contributor.github}
					title={`Go to ${contributor.name}'s profile`}
					class="flex items-center gap-2 text-sm text-slate-800 dark:text-slate-200 opacity-50 hover:opacity-100"
				>
					GitHub
					<Icon icon="charm:link-external" class="" />
				</a>
			</li>
		{/each}
	</ul>
</section>
