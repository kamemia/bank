<script lang="ts">
    import '../app.css';
    import Menu from '../lib/components/Menu/Menu.svelte';
    import PersonsCard from '$lib/components/Cards/PersonsCard.svelte';
</script>

<div class="flex px-4 mx-auto w-full ">
    <main class="lg:ml-72 w-full mx-auto">
      <slot />
    </main>
</div>

<div class="grid grid-rows-3 grid-flow-col gap-4">
  <Menu />
  <div class="absolute top-0 right-0 mt-4 mr-2">
    <PersonsCard />
  </div>

</div>

