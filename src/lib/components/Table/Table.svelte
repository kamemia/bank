<script>
  import { onMount } from 'svelte';

  let jsonData = [];

  onMount(async () => {
    const response = await fetch('/src/data/individualpayments.json'); // Adjust the path based on your actual file location
    jsonData = await response.json();
  });
</script>

<style>
  table {
    width: 100%;
    border-collapse: collapse;
    margin-top: 20px;
  }

  th, td {
    border: 1px solid #ddd;
    padding: 8px;
    text-align: left;
  }

  th {
    background-color: #f2f2f2;
  }
</style>

<table>
  <thead>
    <tr>
      <th>Date</th>
      <th>Type</th>
      <th>Item</th>
      <th>Quantity</th>
      <th>Cost</th>
    </tr>
  </thead>
  <tbody>
    {#if jsonData.length > 0}
      {#each jsonData as item}
        <tr>
          <td>{item.date}</td>
          <td>{item.type}</td>
          <td>{item.item}</td>
          <td>{item.number}</td>
          <td>{item.sum}</td>
        </tr>
      {/each}
    {:else}
      <tr>
        <td colspan="11">Loading...</td>
      </tr>
    {/if}
  </tbody>
</table>
