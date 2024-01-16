<script>
// @ts-nocheck

    import { Card, Listgroup, Avatar } from 'flowbite-svelte';
    let list = [
      {
        img: { src: 'https://www.google.com/url?sa=i&url=https%3A%2F%2Fnordic.ign.com%2Favatar-generations&psig=AOvVaw2EpkuMC43P_Nj4G-IRe4rC&ust=1705411778196000&source=images&cd=vfe&opi=89978449&ved=0CBMQjRxqFwoTCIjatpbA34MDFQAAAAAdAAAAABAD', alt: 'Neil Sims' },
        name: 'Neil Sims',
        email: 'email@windster.com',
        value: '$320'
      },
      {
        img: { src: 'https://www.google.com/url?sa=i&url=https%3A%2F%2Fnordic.ign.com%2Favatar-generations&psig=AOvVaw2EpkuMC43P_Nj4G-IRe4rC&ust=1705411778196000&source=images&cd=vfe&opi=89978449&ved=0CBMQjRxqFwoTCIjatpbA34MDFQAAAAAdAAAAABAD', alt: 'Bonnie Green' },
        name: 'Bonnie Green',
        email: 'email@windster.com',
        value: '$3467'
      },
      {
        img: { src: 'https://www.google.com/url?sa=i&url=https%3A%2F%2Fnordic.ign.com%2Favatar-generations&psig=AOvVaw2EpkuMC43P_Nj4G-IRe4rC&ust=1705411778196000&source=images&cd=vfe&opi=89978449&ved=0CBMQjRxqFwoTCIjatpbA34MDFQAAAAAdAAAAABAD', alt: 'Michael Gough' },
        name: 'Michael Gough',
        email: 'email@windster.com',
        value: '$67'
      }
    ];
  </script>
  
  <Card padding="xl" size="md">
    <div class="flex justify-between items-center mb-4">
      <h5 class="text-xl font-bold leading-none text-gray-900 dark:text-white">Persons</h5>
    </div>
    <Listgroup items={list} let:item class="border-0 dark:!bg-transparent">
      <div class="flex items-center space-x-4 rtl:space-x-reverse">
        <Avatar src={item.img.src} alt={item.img.alt} class="flex-shrink-0" />
        <div class="flex-1 min-w-0">
          <p class="text-sm font-medium text-gray-900 truncate dark:text-white">
            {item.name}
          </p>
          <p class="text-sm text-gray-500 truncate dark:text-gray-400">
            {item.value}
          </p>
        </div>
      </div>
    </Listgroup>
  </Card>