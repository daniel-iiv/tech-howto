<script>
	import PocketBase from 'pocketbase';

    import { ConicGradient } from '@skeletonlabs/skeleton';

	import { onMount } from 'svelte';
	export let data;

    let record = [];

	onMount(async () => {
		const pb = new PocketBase('http://26.118.217.130:8090');
		// const pb = new PocketBase('http://25.65.20.210:8090');
        record = await pb.collection('posts').getOne(data.id);
		console.log(record);
	});

        let conicStops = [
    		{ color: 'transparent', start: 0, end: 25 },
    		{ color: 'rgb(var(--color-primary-500))', start: 75, end: 100 }
    	];
    </script>

    {#if record.title == undefined}
        <div class="flex justify-center items-center h-screen">
            <div class="grid justify-center items-center">
                <ConicGradient stops={conicStops} spin></ConicGradient>
            </div>
        </div>
    {:else}
        <div class="grid justify-center items-center mt-5">
            <h1 class="h1">{record.title}</h1>
            <blockquote class="blockquote mt-5">{record.description}</blockquote>
            <p class="mt-10">{@html record.post}</p>
        </div>
    {/if}

