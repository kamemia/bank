<script>
  import { onMount } from 'svelte';

  let jsonData = [];

  onMount(async () => {
    const response = await fetch('/src/data/individualpayments.json'); 
    jsonData = await response.json();
  });

  function handleRowClick(item) {
    navigate(`/details/${item.id}`); // Replace with the desired route or action
  }

</script>


<style>
  /* Add a container with a fixed height and set overflow to auto for scrolling */
  .table-container {
    height: 800px; /* Adjust the height as needed */
    overflow-y: auto;
    margin-top: 20px;
  }

  table {
    width: 100%;
    border-collapse: collapse;
  }

  th, td {
    border: 1px solid #ddd;
    padding: 8px;
    text-align: left;
    cursor: pointer;
    
  }

  th {
    background-color: #f2f2f2;
    position: static;
    top: 0;
    z-index: 1;
  }
  /* width */
::-webkit-scrollbar {
  width: 10px;
}

/* Track */
::-webkit-scrollbar-track {
  background: #f1f1f1;
}

/* Handle */
::-webkit-scrollbar-thumb {
  background: #888;
}

/* Handle on hover */
::-webkit-scrollbar-thumb:hover {
  background: #555;
}
</style>

<div class="table-container">
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
        <tr on:click={() => handleRowClick(item)}>
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
</div>
