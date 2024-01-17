<script>
  import { onMount } from 'svelte';
  import { createEventDispatcher } from 'svelte';

  let jsonData = [];
  let filteredData = [];
  let filterText = '';

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
  .card {
    display: flex;
    align-items: center;
    justify-content: space-between;
    padding: 10px;
    border: 1px solid #ccc;
    border-radius: 8px;
    margin-bottom: 10px;
    max-width: 300px;
  }

  .avatar {
    width: 50px;
    height: 50px;
    border-radius: 50%;
    margin-right: 10px;
  }

  .info {
    flex-grow: 1;
  }

  .name {
    font-weight: bold;
  }

  .search-input {
    margin-bottom: 10px;
    padding: 5px;
    border: 1px solid #ccc;
    border-radius: 4px;
  }
</style>

<div>
  <input type="text" bind:value={filterText} placeholder="Search..." class="search-input" />

  {#if filteredData.length > 0}
    {#each filteredData as person (person.id)}
      <div class="card" on:click={() => dispatch('cardClick', person)}>
        <img src={`src/data/photos/${person.fname.toLowerCase()}_1.jpg`} alt="Avatar" class="avatar" />
        <div class="info">
          <div class="name">{person.fname} {person.lname}</div>
          <div>${person.money}</div>
        </div>
      </div>
    {/each}
  {:else}
    <p>No matching results</p>
  {/if}
</div>