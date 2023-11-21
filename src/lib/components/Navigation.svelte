<script lang="ts">
  import { getDrawerStore } from '@skeletonlabs/skeleton'

  const drawerSotre = getDrawerStore()

</script>

<nav class="list-nav p-4">
  <ul>
    <li><a on:click={drawerSotre.close} href="/">Home</a></li>
    <li><a on:click={drawerSotre.close} href="/?about=1">About what exactly</a></li>
    <li><a on:click={drawerSotre.close} href="/?help=1">Help me! Help, me! N</a></li>
  </ul>
</nav>
