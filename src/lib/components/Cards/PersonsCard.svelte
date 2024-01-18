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
  .container {
    display: flex;
    flex-direction: column;
    height: 500px;
  }

  .search-bar {
    position: sticky;
    top: 0;
    background-color: #fff; /* Set a background color if needed */
    z-index: 1; /* Ensure the search bar is above other content */
    padding: 10px;
    border-bottom: 1px solid #ccc;
  }

  .cards-container {
    flex-grow: 1;
    overflow-y: scroll;
    padding: 10px; /* Add padding to cards container if necessary */
  }

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

<div class="container">
  <div class="search-bar">
    <input type="text" bind:value={filterText} placeholder="Search..." class="search-input" />
  </div>

  <div class="cards-container">
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
</div>
