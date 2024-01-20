<script>
  
  import {  Label, Input, Textarea, MultiSelect } from 'flowbite-svelte';
	import { createEventDispatcher, onMount } from 'svelte';
    let selected = [];
    let attributes = [
      {value:'new', name:'New'},
      {value:'customer', name:'Customer'},
      {value:'supplier', name:'Supplier'},
      {value:'new', name:'Discount'},
      {value:'old buddy', name:'Old Buddy'},
      {value:'avid supporter', name:'Avid Supporter'},
    ];

    const dispatch = createEventDispatcher();

    let formData = {
      fname: '',
      lname: '',
      birthday:'',
      city:'',
      address:'',
      email:'',
      photo: '',
      position:'',
      notifications:'',
      notes:'',
      tags:''
    }

    let jsonData = [];

    onMount(async () => {
        try {
            const response = await fetch('/src/data/persons.json'); // Adjust the path if needed
            jsonData = await response.json();
            loadPersonData();
            console.log(jsonData); // Check the console to verify that data is loaded
        } catch (error) {
            console.error('Error loading JSON data:', error);
        }
    });

    function loadPersonData(){
      const currentPerson = jsonData[currentIndex];
      if (currentPerson) {
        
      }
    }

    formData = { ...formData, ...jsonData };

    function handleNext() {
        currentIndex = (currentIndex + 1) % jsonData.length;
        loadPersonData();
    }

    function handlePrevious() {
        currentIndex = (currentIndex - 1 + jsonData.length) % jsonData.length;
        loadPersonData();
    }
    
    function handleSubmit() {
      dispatch('formSubmit', { formData });
    }
</script>

<style>
  .container{
    height: 75vh;
  }
</style>

<div class="container">
  <form on:submit={handleSubmit} class="mb-6">
    <div class="grid grid-cols-3 gap-4">
      <div>
        <Label for="fname" class="block mb-2">First name</Label>
        <Input id="fname" name="fname" required bind:value={formData.fname} />
      </div>
      <div class="mb-6">
        <Label for="lname" class="block mb-2">City, country</Label>
        <Input id="lname" name="lname" required bind:value={formData.lname} />
      </div>
      <!-- <div class="mb-6">
        <Label for="title" class="block mb-2">City, country</Label>
        <Input id="title" name="title" required placeholder="Apple Keynote" />
      </div> -->
    </div>
    <div class="grid grid-cols-3 gap-4">
      <div>
        <Label for="title" class="block mb-2">Last name</Label>
        <Input id="title" name="title" required placeholder="Apple Keynote" />
      </div>
      <div class="mb-6">
        <Label for="title" class="block mb-2">Address</Label>
        <Input id="title" name="title" required placeholder="Apple Keynote" />
      </div>
      <MultiSelect items={attributes} bind:value={selected} />
    </div>
    <div class="grid grid-cols-3 gap-4">
      <div class="mb-6">
        <label for="birthday" class="block mb-2">Birthday</label>
        <Input id="date" name="date" required type="date" />
      </div>
      <div class="mb-6">
        <Label for="title" class="block mb-2">Email</Label>
        <Input id="title" name="title" required placeholder="Apple Keynote" />
      </div>
    </div>
    <div class="grid grid-cols-3 gap-4">
      <div class="mb-6">
        <label for="position" class="block mb-2">Birthday</label>
        <Input id="title" name="title" required placeholder="Apple Keynote" />
      </div>
    </div>
    <div class="mb-6">
      <label for="position" class="block mb-2">Notifications</label>
      <div class="flex gap-4">
        <div class="flex items-center">
          <input type="radio" id="yes" name="example">
          <label for="yes" class="ml-1">Yes</label>
        </div>
        <div class="flex items-center">
          <input type="radio" id="no" name="example">
          <label for="no" class="ml-1">No</label>
        </div>
      </div>
    </div>
    
    
    
    
    <div class="mb-6">
        <Label for="notes" class="mb-2">Notes</Label>
        <Textarea id="message" placeholder="Write event description..." rows="4" name="message" />
      </div>

      <button type="button" on:click={handlePrevious}>Previous</button>
        <button type="button" on:click={handleNext}>Next</button>
        <button type="submit">Submit</button>
  </form>
</div>