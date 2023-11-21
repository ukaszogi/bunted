<script lang="ts">
	import '../app.postcss';

	// Floating UI for Popups
	import { computePosition, autoUpdate, flip, shift, offset, arrow } from '@floating-ui/dom';
	import { storePopup } from '@skeletonlabs/skeleton';
	storePopup.set({ computePosition, autoUpdate, flip, shift, offset, arrow });

  // Components
  import { AppShell, AppBar, Avatar } from '@skeletonlabs/skeleton';
  import Navigation from '$lib/components/Navigation.svelte'
  import { Drawer, getDrawerStore } from '@skeletonlabs/skeleton';

  // Types
  import type { DrawerSettings, DrawerStore } from '@skeletonlabs/skeleton';
  
  // Zusatz, Sonstige
  import { initializeStores } from '@skeletonlabs/skeleton';

  initializeStores();

  const drawerStore:DrawerStore = getDrawerStore();
</script>

<Drawer>
  <Navigation />
</Drawer>

<AppShell slotSidebarLeft="w-0 md:w-60 bg-surface-500/10">
	<svelte:fragment slot="header">
    <AppBar>
      <svelte:fragment slot="lead">
        <button class="md:hidden btn-icon variant-soft-tertiary p-2" on:click={drawerStore.open}>
          <svg viewBox="0 0 24 24" fill="none" xmlns="http://www.w3.org/2000/svg">
            <g id="SVGRepo_bgCarrier" stroke-width="0"></g>
            <g id="SVGRepo_tracerCarrier" stroke-linecap="round" stroke-linejoin="round"></g>
            <g id="SVGRepo_iconCarrier">
              <path d="M20 7L4 7" stroke="#1C274C" stroke-width="1.5" stroke-linecap="round"></path>
              <path opacity="0.8" d="M20 12L4 12" stroke="#1C274C" stroke-width="1.5" stroke-linecap="round"></path>
              <path d="M20 17L4 17" stroke="#1C274C" stroke-width="1.5" stroke-linecap="round"></path>
            </g>
          </svg>
        </button>
      </svelte:fragment>
      <h1 class="h1">Bunted in yo ass</h1>
      <svelte:fragment slot="trail">
        <Avatar src="invalid-image.jpg" initials="AB" width="w-12" />
      </svelte:fragment>
    </AppBar>
  </svelte:fragment>
	<svelte:fragment slot="sidebarLeft">
    <Navigation />
  </svelte:fragment>
	<!-- <svelte:fragment slot="sidebarRight">Sidebar Right</svelte:fragment> -->
	<!-- <svelte:fragment slot="pageHeader">Page Header</svelte:fragment> -->
	<!-- Router Slot -->
  <div class="container p-4 mx-auto">
    <slot />
  </div>
	<!-- ---- / ---- -->
	<!-- <svelte:fragment slot="pageFooter">Page Footer</svelte:fragment> -->
	<svelte:fragment slot="footer">Footer</svelte:fragment>
</AppShell>
