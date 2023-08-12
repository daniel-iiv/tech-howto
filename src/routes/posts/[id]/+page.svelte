
<script>
    export let data;

    onMount(async () => {
		const pb = new PocketBase('http://25.65.20.210:8090');
        const record = await pb.collection('posts').getOne(data.id);
		console.log(record);
	});
</script>

<h1>Test {data.id}</h1>