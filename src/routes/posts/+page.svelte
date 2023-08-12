<script>
	import PocketBase from 'pocketbase';

	import { onMount } from 'svelte';

	let records = [];

	onMount(async () => {
		const pb = new PocketBase('http://localhost:8090');
		// const pb = new PocketBase('http://25.65.20.210:8090');
		records = await pb.collection('posts').getFullList({
			sort: '-created',
		});
	});
</script>

<div class="grid grid-flow-col auto-rows-max">
	{#each records as record}
		<div class="card m-4 shadow transition-transform hover:shadow-xl variant-glass variant-outline-primary">
			<section class="p-4"><strong>{record.title}</strong></section>
			<section class="p-4">{record.description}</section>
			<header class="card-footer"><a class="btn btn-sm variant-ghost-primary hover:variant-filled-primary" href="/posts/{record.id}">öffnen</a></header>
		</div>
	{/each}
</div>
