<script lang="ts">
	import '../app.css';
</script>

<svelte:head>
	<link rel="icon" href="/favicon.svg" sizes="any" />
</svelte:head>

<main>
	<div class="max-w-2xl min-h-screen m-auto p-8 prose bg-zinc-100 shadow-md dark:bg-zinc-800">
		<slot />
	</div>
</main>
