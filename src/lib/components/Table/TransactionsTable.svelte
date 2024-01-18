<script>
    import { onMount } from 'svelte';
    import PayPal from '/src/data/images/PayPal.svg';
    import MasterCard from '/src/data/images/MasterCard.svg';
    import Visa from '/src/data/images/Visa.svg';
    import Warning from '/src/data/images/Warning.svg';
    import Tick from '/src/data/images/Tick.svg';
    import Plus from '/src/data/images/Plus.svg';
    import Minus from '/src/data/images/Minus.svg';
  
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
    th{
        padding: 20px;
    }

    .spacer{
        height: 10px;
    }
    ::-webkit-scrollbar-track {
      background: #f1f1f1;
    }
    ::-webkit-scrollbar-thumb {
      background: #888;
    }
    ::-webkit-scrollbar-thumb:hover {
      background: #555;
    }
    ::-webkit-scrollbar {
      width: 5px;
    }
    .success{
      height: 20px;
    }
    .buttons {
    text-align: right;
    }
    .container{
        height: 10vh;
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
    
</style>
  

    <div class="buttons">
      <button class:active={$activeButton === 'all'} on:click={() => { filterType = 'all'; filterData(); }}>All</button>
      <button class:active={$activeButton === 'payments'} on:click={() => { filterType = 'payments'; filterData(); }}>Payments</button>
      <button class:active={$activeButton === 'incoming'} on:click={() => { filterType = 'incoming'; filterData(); }}>Incoming</button>
    </div>

    <div class="spacer"></div>
    <div class="container">
    <div class="relative overflow-x-auto block max-h-screen shadow-md sm:rounded-lg">
      <table class="w-full text-sm text-left rtl:text-right text-gray-500 dark:text-gray-400">
          <thead class="text-xs text-gray-700 uppercase bg-gray-100 dark:bg-gray-700 dark:text-gray-400 sticky top-0">
              <tr>
                  <th scope="col" class="px-6 py-3">
                     #
                  </th>
                  <th scope="col" class="px-6 py-3">
                      Status
                  </th>
                  <th scope="col" class="px-6 py-3">
                      Date
                  </th>
                  <th scope="col" class="px-6 py-3">
                      Method
                  </th>
                  <th scope="col" class="px-6 py-3">
                      Email
                  </th>
                  <th scope="col" class="px-6 py-3">
                    Name
                </th>
                <th scope="col" class="px-6 py-3">
                  Type
                </th>
                <th scope="col" class="px-6 py-3">
                  Sum
                </th>
                <th scope="col" class="px-6 py-3">
                  Left
              </th>
              </tr>
          </thead>
        <tbody class="h-screen overflow-y-auto">
        {#if filteredData.length > 0}
          {#each filteredData as item}
          <tr class="bg-white border-b dark:bg-gray-800 dark:border-gray-700 hover:bg-gray-50 dark:hover:bg-gray-600">
              <th scope="row" class="px-6 py-4 font-medium text-gray-900 whitespace-nowrap dark:text-white">
                {item.id}
              </th>
              <td class="px-6 py-4">
                {#if item.status === 'success'}
                <img src={Tick} class="success" alt="success"/>
                {:else if item.status === 'failed'}
                  <img src={Warning}  class="success" alt="warning"/>
                {:else if item.status === 'waiting'}
                  <ClockSolid class=" text-orange-500 me-4"/>
                {/if}
              </td>
              <td class="px-6 py-4">
                {item.date}
              </td>
              <td class="px-6 py-4">
                {#if item.method === 'PayPal'}
                  <img src={PayPal} class="paypal-logo" alt="paypal" />
                {:else if item.method == 'MasterCard'}
                  <img src={MasterCard} class="mastercard-logo" alt="mastercard"/>
                {:else if item.method == 'Visa'}
                  <img src={Visa} class="visa-logo" alt="visa"/>
                
                {/if}
              </td>
              <td class="px-6 py-4">
                {item.number}
              </td>
              <td class="px-6 py-4">
                {item.name}
              </td>
              <td class="px-6 py-4">
                {#if item.type === 1}
                  <img src={Plus} class="success" alt="Plus"/>
                {:else if item.type === 0}
                  <img src={Minus} class="success" alt="Minus"/>
                {/if}
              </td>
              <td class="px-6 py-4">
                ${item.sum}
              </td>
              <td class="px-6 py-4">
                ${item.left}
              </td>
            </tr>
          {/each}
          <tfoot class="bottom-0 sticky text-xs text-gray-700 bg-gray-100 dark:bg-gray-700 dark:text-gray-400">
            <tr class="font-semibold text-gray-900 dark:text-white">
              <th scope="row" class="px-6 py-3 text-base">Total</th>
              <td class="px-6 py-4">
                ${calculateTotal()}
              </td>
            </tr>
              
          </tfoot>
        {:else}
          <tr>
            <td colspan="8">Loading...</td>
          </tr>
        {/if}
      </tbody>
    </table>
  </div>
</div> 
  
  