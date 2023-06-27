<script lang="ts">
	import UserInfo from '../Components/UserInfo.svelte';
	import Users from '../Components/Users.svelte';
	import Icon from '@iconify/svelte';
	import { contributors, type contributorFace } from '../Data/contributors';
	import { onMount } from 'svelte';
	import Meta from '../Meta/Meta.svelte';

	let isList: boolean = true;
	let user: contributorFace[] | null | undefined = null;

	function handleUerInfoWin(event: any) {
		user = event.detail;
	}

	function handleGrid() {
		isList ? (isList = false) : (isList = true);
	}

	function isUserValid() {
		const check_user = contributors.filter((item) => {
			const savedUserId = item.github.split('/').at(-1);
			const urlUserId = window.location.hash.replaceAll('#', '');
			if (savedUserId === urlUserId) {
				return item;
			}
		});
		return check_user;
	}

	onMount(() => {
		user = isUserValid();
		const handleURLChange = () => {
			user = isUserValid();
		};
		window.addEventListener('popstate', handleURLChange);
		return () => {
			window.removeEventListener('popstate', handleURLChange);
		};
	});
</script>

{#if !user || user.length === 0}
	<Meta />
{/if}

<section class="xl:container mx-auto">
	<header class=" flex justify-between items-center p-3">
		<h2 class="text-black dark:text-white font-medium">
			Total contributor <span class="text-sm">{contributors.length}</span>
		</h2>
		<button type="button" class="w-fit border-none focus:ring-2" on:click={handleGrid}>
			{#if isList}
				<Icon icon="ri:grid-fill" />
			{:else}
				<Icon icon="fa-solid:list" />
			{/if}
		</button>
	</header>
	<hr class="border-slate-500/10" />
	<Users {isList} {contributors} />

	{#if user && user.length > 0}
		<UserInfo contributors={user} on:nameChange={handleUerInfoWin} />
	{/if}
</section>
