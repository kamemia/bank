<script>
    // @ts-nocheck
    
        import { Table, TableBody, TableBodyCell, TableBodyRow, TableHead, TableHeadCell } from 'flowbite-svelte';
    
        import { onMount } from 'svelte';
        let jsonData = [];
    
        onMount(async () => {
          const response = await fetch('/src/data/payments.json');
          jsonData = await response.json();
        });
    </script>
    
    
    
    
    <Table>
      <TableHead>
        <TableHeadCell>#</TableHeadCell>
        <TableHeadCell></TableHeadCell>
        <TableHeadCell>Date</TableHeadCell>
        <TableHeadCell>Payment</TableHeadCell>
        <TableHeadCell></TableHeadCell>
        <TableHeadCell>Purchase</TableHeadCell>
        <TableHeadCell>+/-</TableHeadCell>
        <TableHeadCell>Sum</TableHeadCell>
      </TableHead>
      <TableBody>
        {#if jsonData.length>0}
          {#each jsonData as item}
            <TableBodyRow>
              <TableBodyCell>{item.id}</TableBodyCell>
              <TableBodyCell>{item.status}</TableBodyCell>
              <TableBodyCell>{item.date}</TableBodyCell>
              <TableBodyCell>{item.method}</TableBodyCell>
              <TableBodyCell>{item.number}</TableBodyCell>
              <TableBodyCell>{item.name}</TableBodyCell>
              <TableBodyCell>{item.type}</TableBodyCell>
              <TableBodyCell>{item.sum}</TableBodyCell>
            </TableBodyRow>
          {/each}
          {:else}
            <TableBodyRow>
              <TableBodyCell>Loading ...</TableBodyCell>
            </TableBodyRow>
          {/if}
      </TableBody>
    </Table>
      