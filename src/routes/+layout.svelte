<script>
	import Toasts from '$lib/components/Toasts.svelte';
	import { onMount } from 'svelte';
	import '../app.css';
	import { invalidate } from '$app/navigation';

	let { session, supabase } = $props();

	onMount(() => {
		const { data } = supabase.auth.onAuthStateChange((_, newSession) => {
			if (newSession?.expires_at !== session?.expires_at) {
				invalidate('supabase:auth');
			}
		});

		return () => data.subscription.unsubscribe();
	});
</script>

<Toasts />

<slot />
