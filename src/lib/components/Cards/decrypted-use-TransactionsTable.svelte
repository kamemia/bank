<script>
  import { onMount } from 'svelte';
  import PayPal from '/src/data/images/PayPal.svg';
  import MasterCard from '/src/data/images/MasterCard.svg';
  import Visa from '/src/data/images/Visa.svg';
  import Warning from '/src/data/images/Warning.svg';
  import Tick from '/src/data/images/Tick.svg';

  import { ClockSolid } from 'flowbite-svelte-icons';
  import { writable } from 'svelte/store';
  

  let jsonData = [];
  let filteredData = [];
  let filterType = 'all';
  const total = writable(0);
  const activeButton = writable('all');

  onMount(async () => {
    const response = await fetch('/src/data/payments.json');
    jsonData = await response.json();
    filterData();
  });

  function filterData() {
    if (filterType === 'all' || filterType === 'payments' || filterType === 'incoming') {
      filteredData = jsonData.filter(item => {
        if (filterType === 'all') {
          return true;
        } else if (filterType === 'payments') {
          return item.type === 0;
        } else if (filterType === 'incoming') {
          return item.type === 1;
        }
        return false;
      });

      // Update the active button
      activeButton.set(filterType);

      total.set(calculateTotal());
    }
  }

  function calculateTotal() {
    return filteredData.reduce((total, item) => total + parseFloat(item.sum), 0).toFixed(2);
  }
</script>

<style>
  table {
    width: 100%;
    border-collapse: collapse;
    margin-top: 20px;
    overflow-y: scroll;
    height: 800px;
    display: block;
  }

  thead {
    position: sticky;
    top: 0;
  }

  th, td {
    padding: 20px;
    text-align: left;
  }

  th {
    background-color: #f2f2f2;
  }

  tbody {
    max-height: 700px;
    overflow-y: scroll;
    scrollbar-width: thin; /* For Firefox */
  }

  tbody::-webkit-scrollbar {
    width: 10px;
  }

  tbody::-webkit-scrollbar-thumb {
    background-color: #888;
    border-radius: 5px;
  }

  .footer-row {
    background-color: #f2f2f2; /* Grey background color */
    position: sticky;
    bottom: 0;
  }
  .buttons {
    text-align: right;
}

.buttons button {
    /* Rectangle shape */
    display: inline-block;
    padding: 10px 20px; /* Adjust padding as needed for the desired size */
    border: 1px solid #3498db; /* Border color */
    border-radius: 5px; /* Rounded corners, adjust as needed */

    /* Light shade of blue */
    background-color: #3498db;
    color: #fff; /* Text color */
    cursor: pointer;

    /* Add any additional styling for the buttons if needed */
    margin-left: 5px; /* Add some spacing between the buttons if desired */
}

/* Hover effect */
.buttons button:hover {
    background-color: #2980b9; /* Darker shade of blue on hover, adjust as needed */
}

.buttons button.active {
    background-color: #2980b9;
  }

  .buttons button.active:hover {
    background-color: #1f6694;
  }

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
tbody > tr:hover {
  background-color: #888;
}
.success{
  height: 20px;
}
</style>

<div class="container">
  <div class="buttons">
    <button class:active={$activeButton === 'all'} on:click={() => { filterType = 'all'; filterData(); }}>All</button>
    <button class:active={$activeButton === 'payments'} on:click={() => { filterType = 'payments'; filterData(); }}>Payments</button>
    <button class:active={$activeButton === 'incoming'} on:click={() => { filterType = 'incoming'; filterData(); }}>Incoming</button>
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
        <th>Left</th>
      </tr>
    </thead>
    <tbody class:scrollable-table={filteredData.length > 20}>
      {#if filteredData.length > 0}
        {#each filteredData as item}
          <tr>
            <td>{item.id}</td>
            <td>
              {#if item.status === 'success'}
              <img src={Tick} class="success" alt="success"/>
              {:else if item.status === 'failed'}
                <img src={Warning}  class="success" alt="warning"/>
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
            <td>${item.sum}</td>
            <td>${item.left}</td>
          </tr>
        {/each}
        <tfoot>
          <!-- <tr class="footer-row"> -->
            <td colspan="7"></td>
            <td>Total</td>
            <td>${calculateTotal()}</td>
            <td></td>
          <!-- </tr> -->
        </tfoot>
      {:else}
        <tr>
          <td colspan="8">Loading...</td>
        </tr>
      {/if}
    </tbody>
  </table>
</div>
