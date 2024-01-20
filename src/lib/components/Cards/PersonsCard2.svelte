<script>
    import { onMount } from 'svelte';
    import { createEventDispatcher } from 'svelte';
    import { Tooltip } from 'flowbite-svelte';
  
    let placement = 'left';
    let jsonData = [];
    let filteredData = [];
    let filterText = '';
    let isSearchVisible = false;
  
    const dispatch = createEventDispatcher();
  
    onMount(async () => {
      const response = await fetch('/src/data/persons.json');
      jsonData = await response.json();
      filterData();
    });
  
    function filterData() {
      filteredData = jsonData.filter(person => {
        const fullName = `${person.fname} ${person.lname}`.toLowerCase();
        return fullName.includes(filterText.toLowerCase());
      });
    }
</script>

<style>
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
    .container {
        height: 75vh;
    }
    /* Add the following class to hide the scrollbar */
    .overflow-hidden::-webkit-scrollbar {
        display: none;
    }
</style>

<div class="w-full max-w-xs p-4 bg-white border border-gray-200 rounded-lg shadow sm:p-6 dark:bg-gray-800 dark:border-gray-700">
    <div class="flex items-center justify-between mb-4">
        <h2 class="text-xl font-bold leading-none text-gray-900 dark:text-white">Persons</h2>
        <input
            type="text"
            id="search"
            name="search"
            class="w-full px-3 py-2 border border-gray-300 rounded-md shadow-sm focus:outline-none focus:border-blue-500 focus:ring focus:ring-blue-200 dark:bg-gray-700 dark:text-white"
            bind:value={filterText}
            on:input={filterData}
            placeholder="Enter name to search"
        />
    </div>
    <div class="flow-root max-h-96 overflow-y-auto overflow-hidden" >
        <ul role="list" class="divide-y divide-gray-200 dark:divide-gray-700">
            {#if filteredData.length > 0}
                {#each filteredData as person (person.id)}
                    <li class="py-3 sm:py-4">
                        <div class="flex items-center">
                            <div class="flex-shrink-0">
                                <img class="w-16 h-16 rounded-full" src={`src/data/photos/${person.fname.toLowerCase()}_1.jpg`} alt="Neil image">
                            </div>
                            <div class="flex-1 min-w-0 ms-4">
                                <p class="text-sm font-medium text-gray-900 truncate dark:text-white">
                                    {person.fname} {person.lname}
                                </p>
                                <p class="text-sm text-gray-500 truncate dark:text-gray-400">
                                    ${person.money}
                                </p>
                            </div>
                        </div>
                    </li>
                {/each}
                {:else}
                    <p>No matching results</p>
            {/if}
        </ul>
    </div>
</div>
