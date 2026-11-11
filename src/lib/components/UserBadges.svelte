<script lang="ts">
	import { forumConfig } from '$lib/config';
	import { badgesFor, isAdmin, repFor } from '$lib/ui.svelte';

	let { login }: { login: string | undefined | null } = $props();

	const badges = $derived(login ? badgesFor(login) : []);
	const rep = $derived(repFor(login));
</script>

{#if login && isAdmin(login)}
	<span class="rounded bg-red-600 px-1.5 py-px text-[10px] font-bold text-white">
		{forumConfig.admins.badgeLabel}
	</span>
{/if}
{#each badges as badge (badge)}
	<span class="rounded border border-fd-border bg-fd-muted px-1 py-px text-[10px] font-semibold text-fd-muted-foreground">
		{badge}
	</span>
{/each}
{#if rep !== null}
	<span
		class="rounded border border-fd-border bg-fd-muted px-1 py-px text-[10px] font-semibold text-fd-muted-foreground"
		title="Репутация на форуме"
	>
		{rep} реп.
	</span>
{/if}
