<script>
	import { Skull } from 'lucide-svelte';
	import { onMount } from 'svelte';

	let uses = [
		{ title: 'SvelteKit (Svelte 5!)', url: 'https://kit.svelte.dev/docs/introduction' },
		{ title: 'Tailwind CSS', url: 'https://tailwindcss.com/docs/' },
		{ title: 'DasyUI', url: 'https://daisyui.com/docs/' },
		{ title: 'Lucide', url: 'https://lucide.dev/icons/' }
	];

	let rotation = $state(0);

	onMount(() => {
		const interval = setInterval(() => {
			rotation += 2; // Adjust rotation speed here
			if (rotation >= 360) {
				rotation = 0;
			}
		}, 20); // Adjust rotation interval here

		return () => clearInterval(interval);
	});
</script>

<main class="flex h-screen justify-center">
	<article class="flex justify-center items-center">
		<div class="card w-96 bg-base-100 shadow-xl">
			<div class="card-body">
				<h1 class="card-title justify-center">
					Hello From <b
						class=" [&::selection]:text-base-content relative col-start-1 row-start-1 bg-[linear-gradient(90deg,theme(colors.error)_0%,theme(colors.secondary)_9%,theme(colors.secondary)_42%,theme(colors.primary)_47%,theme(colors.accent)_100%)] bg-clip-text [-webkit-text-fill-color:transparent] [&::selection]:bg-blue-700/20 [@supports(color:oklch(0_0_0))]:bg-[linear-gradient(90deg,oklch(var(--s))_4%,color-mix(in_oklch,oklch(var(--s)),oklch(var(--er)))_22%,oklch(var(--p))_45%,color-mix(in_oklch,oklch(var(--p)),oklch(var(--a)))_67%,oklch(var(--a))_100.2%)]"
						>SvelteKit</b
					>
				</h1>
				<h2>It use:</h2>
				<ul class="list-disc">
					{#each uses as u}
						<li><a class="link" href={u.url}>{u.title}</a></li>
					{/each}
					<br />
					<div class="flex justify-center">
						<Skull size="30" style="transform: rotate({rotation}deg);" />
					</div>
				</ul>
			</div>
		</div>
	</article>
</main>
