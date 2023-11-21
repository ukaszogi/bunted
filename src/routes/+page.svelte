<script lang="ts">
  import { noteStore } from '$lib/stores.ts';
  import { getModalStore, getToastStore, type ModalSettings } from '@skeletonlabs/skeleton';

  const modalStore = getModalStore();
  const toastStore = getToastStore();

  function deleteNote(noteId: string): void {
    const confirmDelete: ModalSettings = {
      type: "confirm",
      title: "Delete Note",
      body: "Are you sure you want to delete the note",
      response: (r: boolean) => {
        if (r) {
          noteStore.update((notes) => notes.filter((note) => note.id !== noteId))
          toastStore.trigger({
            message: "Note deleted successfully",
            background: "variant-ghost-success"
          })
        } else {
          toastStore.trigger({
            message: "Note not deleted",
            background: "variant-ghost-error"
          })
        }
      }
    }    
    modalStore.trigger(confirmDelete)
  }
</script>

<div class="container h-full mx-auto flex flex-col gap-8">
  <div class="container flex items-center justify-between">
    <h2 class="h2">Notes</h2>
    <a href="/new" class="btn bg-gradient-to-tr variant-gradient-primary-tertiary hover:scale-110 transform-gpu"> New Note </a>
  </div>
  <div class="grid grid-cols-3 gap-4">
    {#each $noteStore as note}
      <div class="card p-4 variant-ghost-warning flex flex-col gap-2 relative">
        <button on:click={() => deleteNote(note.id)} class="btn-icon-sm variant-filled-error absolute -top-1.5 -right-1.5">X</button>
        <div>{note.content}</div>
        <div class="flex gap-1 flex-wrap">
          {#each note.tags as tag}
            <span class="chip cursor-default variant-filled-tertiary">{tag}</span>
          {/each}
        </div>
      </div>
    {/each}
  </div>
</div>

<style lang="postcss">
  a.btn, button.btn {
    @apply hover:scale-110 transform-gpu;
  }
</style>
