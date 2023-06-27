<script lang="ts">
	import type { contributorFace } from '../Data/contributors';
	import type { UserFace } from '../Types/userFace';
	import { createEventDispatcher, onMount } from 'svelte';
	import { goto } from '$app/navigation';
	import Meta from '../Meta/Meta.svelte';
	import Icon from '@iconify/svelte';
	export let contributors: contributorFace[];

	const dispatch = createEventDispatcher();
	const userId = contributors[0].github.split('/').at(-1);
	let userData: null | UserFace = null;
	let opacity: number = 0;

	function handleClick() {
		dispatch('nameChange', null);
		goto('/');
	}

	async function fetchData() {
		try {
			const response = await fetch(`https://api.github.com/users/${userId}`);
			const data = await response.json();
			userData = data;
		} catch (error) {
			console.error('Error:', error);
		}
	}

	onMount(async () => {
		await fetchData();
	});
</script>

<Meta title={userData?.name} description={userData?.bio} />

<section
	class={`w-full h-screen flex p-2 items-center justify-center fixed top-0 left-0 bg-white/50 dark:bg-black/50 backdrop-blur-sm z-50 overflow-auto ${opacity}`}
>
	<button
		class="absolute top-2 right-2 p-1 w-fit group bg-slate-200 dark:bg-slate-900 border-2 border-transparent hover:border-white dark:hover:border-black shadow-lg shadow-slate-500/20 hover:shadow-slate-500/40 focus:ring-2"
		on:click={handleClick}
	>
		<Icon icon="iconamoon:close" class="group-hover:scale-125" />
	</button>

	{#if userData}
		<article
			class="px-2 sm:p-3 md:p-5 border-2 rounded-xl max-w-[640px] w-full mx-auto sm:flex items-start sm:gap-3 md:gap-5 bg-slate-100 dark:bg-slate-900 border-transparent hover:border-white dark:hover:border-black shadow-lg shadow-slate-500/20 hover:shadow-slate-500/30"
		>
			<figure class="max-w-[100px] aspect-square rounded-full shadow-lg shadow-slate-500">
				<img src={userData.avatar_url} alt={userData.name} class="" />
			</figure>
			<section class="w-full mt-5">
				<h2 class="text-2xl sm:text-xl font-bold text-black dark:text-white" title={userData.name}>
					{userData.name}
				</h2>
				<h3 class="sm:text-xs text-black dark:text-white opacity-70">@{userData.login}</h3>
				{#if userData.bio}
					<p class="sm:text-sm text-black dark:text-white py-2">{userData.bio}</p>
				{/if}
				<ul
					class="sm:text-xs p-2 px-4 shadow-lg shadow-slate-500/20 mt-2 grid grid-cols-3 gap-5 items-center rounded-lg bg-white dark:bg-black"
				>
					<li class="list-none text-black dark:text-white opacity-70">
						Followers <br /> <span class="font-bold"> {userData.followers}</span>
					</li>
					<li class="list-none text-black dark:text-white opacity-70">
						Following <br /> <span class="font-bold">{userData.following}</span>
					</li>
					<li class="list-none text-black dark:text-white opacity-70">
						Repos <br /> <span class="font-bold">{userData.public_repos}</span>
					</li>
				</ul>

				<ul class="grid grid-cols-2 mt-5 sm:text-sm">
					{#if userData.location}
						<li
							class="flex items-center gap-2 text-black dark:text-white opacity-80"
							title={`location ${userData.location}`}
						>
							<Icon icon="carbon:location-filled" />
							<span>{userData.location}</span>
						</li>
					{/if}
					{#if userData.twitter_username}
						<li class="flex items-center gap-2 text-black dark:text-white opacity-80">
							<Icon icon="uil:twitter" />
							<a
								href={`http://twitter.com/${userData.twitter_username}`}
								target="_blank"
								title={`Twitter`}
								rel="noopener noreferrer">Twitter</a
							>
						</li>
					{/if}
					{#if userData.blog}
						<li
							class="flex items-center gap-2 text-black dark:text-white opacity-80"
							title={`Website`}
						>
							<Icon icon="tabler:world-www" />
							<a href={userData.blog} target="_blank" rel="noopener noreferrer">Website</a>
						</li>
					{/if}
					<li class="flex items-center gap-2 text-black dark:text-white opacity-80">
						<Icon icon="uil:github" />
						<a
							href={`https://github.com/${userData.login}`}
							target="_blank"
							title={`Github`}
							rel="noopener noreferrer">Github</a
						>
					</li>
				</ul>
			</section>
		</article>
	{:else}
		<span
			class="w-8 aspect-square border-2 rounded-full border-slate-500 border-t-transparent animate-spin"
		/>
	{/if}
</section>
