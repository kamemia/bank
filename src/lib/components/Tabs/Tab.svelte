<script>
    import { Drawer, Button, CloseButton, Label, Input, Textarea } from 'flowbite-svelte';
    import { InfoCircleSolid, UserPlusSolid, CalendarEditSolid } from 'flowbite-svelte-icons';
</script>

<form action="#" class="mb-6">
    <div class="mb-6">
      <Label for="title" class="block mb-2">Title</Label>
      <Input id="title" name="title" required placeholder="Apple Keynote" />
    </div>
    <div class="mb-6">
      <Label for="description" class="mb-2">Description</Label>
      <Textarea id="message" placeholder="Write event description..." rows="4" name="message" />
    </div>
    <div class="mb-6">
      <Input id="date" name="date" required type="date" />
    </div>
    <div class="mb-4">
      <div class="relative">
        <Input noBorder id="search" placeholder="Add guest email" class="p-3" />
        <Button textSize="text-sm" class="absolute inline-flex items-center px-3 py-1 text-sm font-medium text-white bg-primary-700 rounded-lg end-2 bottom-2 hover:bg-primary-800 focus:ring-4 focus:outline-none focus:ring-primary-300 dark:bg-primary-600 dark:hover:bg-primary-700 dark:focus:ring-primary-800" type="submit">
          <UserPlusSolid class="w-3 h-3 me-1.5 text-white" />Add
        </Button>
      </div>
    </div>
    <div class="flex mb-4 -space-x-4 rtl:space-x-reverse">
      <img class="w-8 h-8 border-2 border-white rounded-full dark:border-gray-800" src="/images/profile-picture-1.webp" alt="" />
      <img class="w-8 h-8 border-2 border-white rounded-full dark:border-gray-800" src="/images/profile-picture-2.webp" alt="" />
      <img class="w-8 h-8 border-2 border-white rounded-full dark:border-gray-800" src="/images/profile-picture-3.webp" alt="" />
      <img class="w-8 h-8 border-2 border-white rounded-full dark:border-gray-800" src="/images/profile-picture-4.webp" alt="" />
    </div>
    <Button type="submit" class="w-full">
      <CalendarEditSolid class="w-3.5 h-3.5 me-2.5 text-white" /> Create event
    </Button>
  </form>