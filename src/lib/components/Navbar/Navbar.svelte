<script>
    import { DarkMode, Navbar, NavUl, NavLi, NavBrand, NavHamburger} from 'flowbite-svelte';
    let darkmodebtn =
    'text-gray-500 dark:text-gray-300 hover:bg-gray-100 dark:hover:bg-gray-700 focus:outline-none focus:ring-4 focus:ring-gray-200 dark:focus:ring-gray-700 rounded-lg text-lg p-2.5 fixed right-4  z-50';
    let navClass = 'bg-ricecake border-gray-200 p-2 border-b rounded  dark:bg-blackpearl';
</script>

<Navbar let:hidden let:toggle {navClass}>
  <NavHamburger on:click={toggle} />
  <NavUl {hidden}>
    <NavLi href="#" active={true} class="text-lg">Webix</NavLi>
  </NavUl>
</Navbar>