<style lang="scss">
</style>

<script lang="ts" context="module">
	export async function load({ page, fetch }) {
		return {
			props: {
				//users: await fetch('/users.json').then((res) => res.json()),
				users: await fetch('http://localhost:5000/yfin/zs').then((res) => res.json()),
			},
		};
	}
</script>

<script lang="ts">
	// Sevelte Imports
	// Utils

	// Components
	import HeadTags from '$components/head-tags/HeadTags.svelte';

	// Models
	import type { UserModel } from '$models/classes/user.model';
	import type { IMetaTagProperties } from '$models/interfaces/imeta-tag-properties.interface';
	// End: Local Imports

	// Start: Exported properties
	export let users: UserModel[] = [];
	export let stocks: {}
	// End: Exported properties

	// Start: Local component properties

	/**
	 * @type {IMetaTagProperties}
	 */
	const metaData: Partial<IMetaTagProperties> = {
		title: 'Users | Sveltekit',
		description:
			'Sveltekit starter project created with sveltekit, typescript, tailwindcss, postcss, husky, and storybook. The project has the structure set up for the scaleable project. (sveltekit, typescript, tailwindcss, postcss, husky, Storybook).',
		url: '/users',
		keywords: ['sveltekit', 'sveltekit starter', 'sveltekit starter users'],
		searchUrl: '/users',
	};
	console.log(users);
</script>

<!-- Start: Header Tag -->
<HeadTags metaData="{metaData}" />
<!-- End: Header Tag -->
<div class="flex flex-col justify-center items-start max-w-2xl mx-auto mb-16">
	<h1 class="font-bold text-3xl md:text-5xl tracking-tight mb-4 dark:text-white"> Users </h1>
	<div class="mb-8 prose leading-6 text-gray-600 dark:text-gray-400">
		<p>
			This page is setup in a way where you can programmatically route to sub routes. Click on each user card to
			go to there details view.
		</p>
		<div class="flex relative mx-auto w-1/4 max-w-md">
			<input class="border-2 border-primary bg-red transition h-12 px-5 pr-16 rounded-md focus:outline-none w-full text-black text-lg " type="search" name="search" placeholder="Search" />
			<button type="submit" class="absolute right-2 top-3 mr-4">
			  <svg class="text-black h-6 w-6 fill-current" xmlns="http://www.w3.org/2000/svg" xmlns:xlink="http://www.w3.org/1999/xlink" version="1.1" id="Capa_1" x="0px" y="0px" viewBox="0 0 56.966 56.966" style="enable-background:new 0 0 56.966 56.966;" xml:space="preserve" width="512px" height="512px">
				<path d="M55.146,51.887L41.588,37.786c3.486-4.144,5.396-9.358,5.396-14.786c0-12.682-10.318-23-23-23s-23,10.318-23,23  s10.318,23,23,23c4.761,0,9.298-1.436,13.177-4.162l13.661,14.208c0.571,0.593,1.339,0.92,2.162,0.92  c0.779,0,1.518-0.297,2.079-0.837C56.255,54.982,56.293,53.08,55.146,51.887z M23.984,6c9.374,0,17,7.626,17,17s-7.626,17-17,17  s-17-7.626-17-17S14.61,6,23.984,6z" />
			  </svg>
			</button>
		  </div>
		<ul>
			{#each users as user}
				<li>{JSON.stringify(user)}</li>
			{/each}
		</ul>
	</div>
	{#if users.length > 0}
		{#each users as user}
			<a sveltekit:prefetch href="{`/users/${user.id}`}" class="w-full">
				<div
					class="mb-4 hover:transition-shadow hover:shadow dark:hover:transition-shadow dark:hover:shadow flex items-center border border-gray-200 dark:border-gray-800 rounded p-4"
				>
					<div class="h-14 w-14 ml-2 mr-4 flex-shrink-0">
						<span class="sr-only">{user.name}</span>
						<svg
							fill="none"
							stroke="currentColor"
							stroke-linecap="round"
							stroke-linejoin="round"
							stroke-width="2"
							class="h-14 w-14 min-w-sm dark:text-gray-400"
							viewBox="0 0 24 24"
						>
							<path d="M20 21v-2a4 4 0 00-4-4H8a4 4 0 00-4 4v2"></path>
							<circle cx="12" cy="7" r="4"></circle>
						</svg>
					</div>
					<div>
						<h3 class="text-lg font-bold tracking-tight text-gray-900 dark:text-gray-100">
							{user.name}
						</h3>
						<p class="leading-5 text-gray-700 dark:text-gray-300">
							{user.job}
						</p>
					</div>
				</div>
			</a>
		{/each}
	{/if}
</div>
