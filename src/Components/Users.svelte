<script lang="ts">
	import Icon from '@iconify/svelte';
	import type { contributorFace } from '../Data/contributors';
	export let contributors: contributorFace[];
	export let isList: boolean;
</script>

<ul class={`grid ${!isList ? 'md:grid-cols-2' : 'grid-cols-1'}`}>
	{#each contributors as contributor}
		<li
			class="flex hover:bg-slate-100 dark:hover:bg-slate-900 m-0 items-center group relative"
			title={`${contributor.name}'s profile`}
		>
			<a
				href={`/#${contributor.github.split('/').at(-1)}`}
				class="w-full flex gap-2 items-center h-full p-3 !bg-transparent focus:ring-2"
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
			</a>
			<a
				href={contributor.github}
				title={`${contributor.name}'s github`}
				target="_blank"
				class="h-full flex items-center gap-2 text-sm text-slate-800 dark:text-slate-200 opacity-50 hover:opacity-100 p-3 !bg-transparent focus:ring-2"
			>
				GitHub
				<Icon icon="charm:link-external" class="" />
			</a>
		</li>
	{/each}
</ul>
