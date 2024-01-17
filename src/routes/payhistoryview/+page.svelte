<script>
    import Menu from '$lib/components/Menu/Menu.svelte'
    import Table from '$lib/components/Table/Table.svelte'
    import PersonsCard from '$lib/components/Cards/PersonsCard.svelte';
</script>

<Menu/>

<div class="grid grid-cols-5 grid-rows-5 gap-4">
    <div class="col-span-4 row-span-5"><Table/></div>
    <div class="row-span-5 col-start-5"><PersonsCard/></div>
</div>
  