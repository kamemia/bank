<script>
import Left from '/src/data/images/Left.svg';
import Right from '/src/data/images/Right.svg';
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
th{
    padding: 20px;
}
.container{
    height: 75vh;
}
.success{
      height: 20px;
    }
div{
    height: 75vh;
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

</style>

<div class="container">
<div class="relative overflow-x-auto block max-h-screen shadow-md sm:rounded-lg">
    <table class="w-full text-sm text-left rtl:text-right text-gray-500 dark:text-gray-400">
        <thead class="text-xs text-gray-700 uppercase bg-gray-100 dark:bg-gray-700 dark:text-gray-400 sticky top-0">
            <tr>
                <th scope="col" class="px-6 py-3">
                   Date
                </th>
                <th scope="col" class="px-6 py-3">
                    Type
                </th>
                <th scope="col" class="px-6 py-3">
                    Item
                </th>
                <th scope="col" class="px-6 py-3">
                    Quantity
                </th>
                <th scope="col" class="px-6 py-3">
                    Cost
                </th>
            </tr>
        </thead>
        <tbody class="h-screen overflow-y-auto">
            {#if jsonData.length > 0}
                {#each jsonData as item}
                <tr class="bg-white border-b dark:bg-gray-800 dark:border-gray-700 hover:bg-gray-50 dark:hover:bg-gray-600">
                <th scope="row" class="px-6 py-4 font-medium text-gray-900 whitespace-nowrap dark:text-white">
                    {item.date}
                </th>
                <td class="px-6 py-4">
                    {#if item.type === 1}
                        <img src={Left} class="success" alt="Plus"/>
                    {:else if item.type === 0}
                        <img src={Right} class="success" alt="Minus"/>
                    {/if}
                </td>
                <td class="px-6 py-4">
                    {item.item}
                </td>
                <td class="px-6 py-4">
                    {item.number}
                </td>
                <td class="px-6 py-4">
                    {item.sum}
                </td>
            </tr>
            {/each}
            {:else}
            <tr class="bg-white dark:bg-gray-800">
               <td class="px-6 py-4">Loading</td>
            </tr>
            {/if}
        </tbody>
        <tfoot class="bottom-0 sticky text-xs text-gray-700 bg-gray-100 dark:bg-gray-700 dark:text-gray-400">
            <tr class="font-semibold text-gray-900 dark:text-white">
                <th scope="row" class="px-6 py-3 text-base">Total</th>
            </tr>
        </tfoot>
    </table>
</div>
</div>
