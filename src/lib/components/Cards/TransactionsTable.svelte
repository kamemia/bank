<script>
  import { onMount } from 'svelte';
  import PayPal from '/src/data/images/PayPal.svg';
  import MasterCard from '/src/data/images/MasterCard.svg';
  import Visa from '/src/data/images/Visa.svg';
  import beer from 'svelte-awesome/icons/beer';
  import Icon from 'svelte-awesome/components/Icon.svelte';
  import { ClockSolid } from 'flowbite-svelte-icons';

  let jsonData = [];
  let filteredData = [];
  let filterType = 'all';

  onMount(async () => {
    const response = await fetch('/src/data/payments.json');
    jsonData = await response.json();
    filterData();
  });

  function filterData() {
    if (filterType === 'all') {
      filteredData = jsonData;
    } else {
      filteredData = jsonData.filter(item => item.type === filterType);
    }
  }
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

<div class="container">
  <div class="buttons">
    <button on:click={() => { filterType = 'all'; filterData(); }}>All</button>
    <button on:click={() => { filterType = 'payments'; filterData(); }}>Payments</button>
    <button on:click={() => { filterType = 'incoming'; filterData(); }}>Incoming</button>
  </div>

  <table>
    <thead>
      <tr>
        <th>#</th>
        <th>Status</th>
        <th>Date</th>
        <th>Method</th>
        <th>Email</th>
        <th>Name</th>
        <th>Type</th>
        <th>Sum</th>
      </tr>
    </thead>
    <tbody class:scrollable-table={filteredData.length > 20}>
      {#if filteredData.length > 0}
        {#each filteredData as item}
          <tr>
            <td>{item.id}</td>
            <td>
              {#if item.status === 'success'}
                <Icon data="{beer}" alt='success'/>
              {:else if item.status === 'failed'}
                <Icon data="{beer}" />
              {:else if item.status === 'waiting'}
                <ClockSolid class=" text-orange-500 me-4"/>
              {/if}
            </td>
            <td>{item.date}</td>
            <td>
              {#if item.method === 'PayPal'}
                <img src={PayPal} class="paypal-logo" alt="paypal" />
              {:else if item.method == 'MasterCard'}
                <img src={MasterCard} class="mastercard-logo" alt="mastercard"/>
              {:else if item.method == 'Visa'}
                <img src={Visa} class="visa-logo" alt="visa"/>
              
              {/if}
              </td>
            <td>{item.number}</td>
            <td>{item.name}</td>
            <td>{item.type}</td>
            <td>{item.sum}</td>
          </tr>
        {/each}
      {:else}
        <tr>
          <td colspan="8">Loading...</td>
        </tr>
      {/if}
    </tbody>
  </table>
</div>
