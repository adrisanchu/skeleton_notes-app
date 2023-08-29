<script lang="ts">
	import { InputChip } from '@skeletonlabs/skeleton';
	import { noteStore } from '../../stores';
	let tags: string[] = [];
	let content: string;

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
	}
</script>

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
