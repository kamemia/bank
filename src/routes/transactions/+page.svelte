<script lang="ts">
    import TransactionsTable from '$lib/components/Table/TransactionsTable.svelte';
    import Menu from '$lib/components/Menu/Menu.svelte'
    import CalenderCard from '$lib/components/Cards/CalenderCard.svelte';
    
</script>


<Menu/>

<div class="grid grid-cols-5 grid-rows-5 gap-4">
    <div class="col-span-4 row-span-5"><TransactionsTable/></div>
    <div class="row-span-4 col-start-5"><CalenderCard/></div>
</div>

    