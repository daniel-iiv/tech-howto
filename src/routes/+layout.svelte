<script>
	import { LightSwitch } from '@skeletonlabs/skeleton';
	// The ordering of these imports is critical to your app working properly
	import '@skeletonlabs/skeleton/themes/theme-skeleton.css';
	// If you have source.organizeImports set to true in VSCode, then it will auto change this ordering
	import '@skeletonlabs/skeleton/styles/skeleton.css';
	// Most of your app wide CSS should be put in this file
	import '../app.postcss';
	import { AppShell, AppBar } from '@skeletonlabs/skeleton';
</script>

<!-- App Shell -->
<AppShell>
	<svelte:fragment slot="header">
		<!-- App Bar -->
		<AppBar>
			<svelte:fragment slot="lead">
				<a href="/"><strong class="text-xl uppercase">Tech-Howto 🧑‍💻</strong></a>
				<a
					class="ml-4 btn btn-sm variant-ghost-surface hover:bg-violet-400 transition-transform hover:scale-110 hover:shadow-lg hover:rotate-6"
					href="/posts"
				>
					Beiträge
				</a>
				<a
					class="ml-2 btn btn-sm variant-ghost-surface hover:bg-violet-400 transition-transform hover:scale-110 hover:shadow-lg hover:rotate-6"
					href="https://github.com/skeletonlabs/skeleton"
				>
					Tools
				</a>
			</svelte:fragment>
			<svelte:fragment slot="trail">
				<!-- <a
					class="btn btn-sm variant-ghost-surface"
					href="https://github.com/skeletonlabs/skeleton"
					target="_blank"
					rel="noreferrer"
				>
					GitHub
				</a> -->
				<LightSwitch />
			</svelte:fragment>
		</AppBar>
	</svelte:fragment>
	<!-- Page Route Content -->
	<slot />
</AppShell>
