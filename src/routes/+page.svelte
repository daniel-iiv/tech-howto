<!-- YOU CAN DELETE EVERYTHING IN THIS PAGE -->

<script>
	import PocketBase from 'pocketbase';

	import { onMount } from 'svelte';

	let records = [];

	onMount(async () => {
		const pb = new PocketBase('http://localhost:8090');
		records = await pb.collection('posts').getFullList({
			sort: '-created',
		});
		console.log(records);
	});

</script>

<div class="grid h-56 place-items-center">
	<h2 class="h2">Willkommen bei Tech-HowTo!</h2>
</div>

<div class="container h-full mx-auto flex justify-center items-center">
	<div class="space-y-10 text-center flex flex-col items-center">
		{#each records as record}
			<div class="card">
				<!-- <header class="card-header">{record.title}</header> -->
				<section class="p-4">{record.title}</section>
				<!-- <section class="p-4">{@html record.post}</section> -->
			</div>
		{/each}
	</div>
</div>

<style lang="postcss">
	figure {
		@apply flex relative flex-col;
	}
	figure svg,
	.img-bg {
		@apply w-64 h-64 md:w-80 md:h-80;
	}
	.img-bg {
		@apply absolute z-[-1] rounded-full blur-[50px] transition-all;
		animation: pulse 5s cubic-bezier(0, 0, 0, 0.5) infinite,
			glow 5s linear infinite;
	}
	@keyframes glow {
		0% {
			@apply bg-primary-400/50;
		}
		33% {
			@apply bg-secondary-400/50;
		}
		66% {
			@apply bg-tertiary-400/50;
		}
		100% {
			@apply bg-primary-400/50;
		}
	}
	@keyframes pulse {
		50% {
			transform: scale(1.5);
		}
	}
</style>
