<script>
    import {  Label, Input, Textarea, MultiSelect } from 'flowbite-svelte';
    let selected = [];
    let attributes = [
      {value:'new', name:'New'},
      {value:'customer', name:'Customer'},
      {value:'supplier', name:'Supplier'},
      {value:'new', name:'Discount'},
      {value:'old buddy', name:'Old Buddy'},
      {value:'avid supporter', name:'Avid Supporter'},
    ];
    
</script>

<style>
  .container{
    height: 75vh;
  }
</style>

<div class="container">
  <form action="#" class="mb-6">
    <div class="grid grid-cols-3 gap-4">
      <div>
        <Label for="title" class="block mb-2">First name</Label>
        <Input id="title" name="title" required placeholder="Apple Keynote" />
      </div>
      <div class="mb-6">
        <Label for="title" class="block mb-2">City, country</Label>
        <Input id="title" name="title" required placeholder="Apple Keynote" />
      </div>
      <div class="mb-6">
        <Label for="title" class="block mb-2">City, country</Label>
        <Input id="title" name="title" required placeholder="Apple Keynote" />
      </div>
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
  </form>
</div>