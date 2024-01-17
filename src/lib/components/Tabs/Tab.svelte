<script>
    import { Drawer, Button, CloseButton, Label, Input, Textarea } from 'flowbite-svelte';
    import { InfoCircleSolid, UserPlusSolid, CalendarEditSolid } from 'flowbite-svelte-icons';
</script>

<form action="#" class="mb-6">
    <div class="mb-6">
      <Label for="title" class="block mb-2">First name</Label>
      <Input id="title" name="title" required placeholder="Apple Keynote" />
    </div>
    <div class="mb-6">
        <Label for="title" class="block mb-2">Last name</Label>
        <Input id="title" name="title" required placeholder="Apple Keynote" />
    </div>
    <div class="mb-6">
        <label for="birthday" class="block mb-2">Birthday</label>
        <Input id="date" name="date" required type="date" />
    </div>
    <div class="mb-6">
        <Label for="notes" class="mb-2">Notes</Label>
        <Textarea id="message" placeholder="Write event description..." rows="4" name="message" />
      </div>
    
    <Button type="submit" class="w-full">
      <CalendarEditSolid class="w-3.5 h-3.5 me-2.5 text-black" /> Create event
    </Button>
  </form>