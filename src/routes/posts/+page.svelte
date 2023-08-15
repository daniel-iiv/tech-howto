<script>
	import PocketBase from 'pocketbase';

	import { onMount } from 'svelte';

	let records = [];
	let tags = [];
	let tagNames = {};

	onMount(async () => {
		const pb = new PocketBase('http://localhost:8090');
		tags = await pb.collection('tags').getFullList();
		console.log(tags);
		
		records = await pb.collection('posts').getFullList({
			fields: 'id,title,description,created,tags',
			sort: '-created',
			// expand: 'tags'
		});

		tags.forEach(element => {
			tagNames[element.id] = element.name;
		});
		console.log(tagNames);

	});


	function localDate(date) {
		return new Date(date).toLocaleDateString();
	}
</script>

<div class="grid grid-flow-row w-full 2xl:w-9/12 mx-auto">
	{#each records as record}
	<div class="card p-4 m-4 shadow transition-transform hover:shadow-xl variant-glass variant-outline-primary overflow-hidden">
		<div class="grid grid-cols-3">
			<div class="container h-full w-full" style="max-width: 100%;max-height: 100%">
				<img class="object-contain h-full w-full" src="https://placehold.co/600x400.png" alt="">
			</div>
			<div>
				<section class="h2 ml-2"><strong>{record.title}</strong></section>
				<section class="py-4 ml-2">{record.description}</section>
				<!-- {#each record.expand.tags as tag}
				<span class="badge variant-filled mx-auto">{tag.name}</span>
				{/each} -->
				{#each record.tags as tag}
					<span class="badge variant-filled ml-2">{tagNames[tag]}</span>
				{/each}
			</div>
			<div>
				<section class="py-4 text-end">veröffentlicht am {localDate(record.created)}</section>
				<a class="btn btn-sm variant-ghost-primary hover:variant-filled-primary" href="/posts/{record.id}">mehr</a>
			</div>
		</div>
	</div>
	{/each}
</div>
