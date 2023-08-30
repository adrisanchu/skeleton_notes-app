<script lang="ts">
	import { InputChip, toastStore, type ToastSettings } from '@skeletonlabs/skeleton';
	import { noteStore } from '$lib/stores';
	import { goto } from '$app/navigation';
	let tags: string[] = [];
	let content: string;

	const t: ToastSettings = {
		message: 'Note created successfully!',
		background: 'variant-filled-success'
	};

	function createNote(): void {
		noteStore.update((notes) => [
			...notes,
			{
				id: crypto.randomUUID(),
				content,
				tags
			}
		]);
		// reset input form
		content = '';
		tags = [];
		// display success notification
		toastStore.trigger(t);
		// navigate to main page
		goto('/');
	}
</script>

<svelte:head>
	<title>Noted - New</title>
</svelte:head>

<div class="container h-full mx-auto gap-8 flex flex-col">
	<form class="card p-4 flex flex-col gap-3">
		<h2>New Note</h2>
		<textarea
			bind:value={content}
			class="textarea"
			rows="5"
			placeholder="Enter some long form content."
		/>
		<InputChip bind:value={tags} name="tags" placeholder="Tags..." />
		<button type="button" on:click={createNote} class="btn variant-ghost-primary self-end"
			>Create Note</button
		>
	</form>
</div>
