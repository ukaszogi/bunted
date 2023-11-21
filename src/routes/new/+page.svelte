<script lang="ts">
  import {noteStore} from '$lib/stores.ts'
  import { InputChip, getToastStore } from '@skeletonlabs/skeleton';
  import type { ToastSetting } from '@skeletonlabs/skeleton'

  const toastStore = getToastStore()

  let tags: string[] = [];
  let content: string;

  function createNote(): void {
    noteStore.update((notes) => [...notes, {
      id: crypto.randomUUID(),
      content,
      tags
    }]);
    content = "";
    tags = [];
  }
</script>

<div class="container h-full mx-auto gap-8 flex flex-col">
  <form class="card p-4 flex flex-col gap-3">
    <h2 class="h2">New Note</h2>
    <textarea class="textarea" rows="5" bind:value={content}/>
    <InputChip name="tags" bind:value={tags} placeholder="Add Tags..." />
    <button on:click={createNote} type="button" class="btn variant-ghost-primary self-end">Create Note</button>
  </form>
</div>
