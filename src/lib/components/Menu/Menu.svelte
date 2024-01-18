<script>
  import { onMount } from 'svelte';
  import { goto } from '$app/navigation';
  import { CalendarEditOutline, CloseOutline, HomeSolid } from 'flowbite-svelte-icons';
	import { MegaMenu } from 'flowbite-svelte';

  let navActive = false;

  const toggleNav = () => {
    navActive = !navActive;
  };

  // A function to navigate to a different page and update the active class
  const navigateTo = (/** @type {string | URL} */ path) => {
    goto(path);
    updateActiveClass();
  };

  // Function to update the active class based on the current route
  const updateActiveClass = () => {
    const currentPath = window.location.pathname;
    const links = document.querySelectorAll('.menu__Link');

    links.forEach((link) => {
      const linkPath = link.getAttribute('href');

      if (currentPath === linkPath) {
        link.classList.add('active');
      } else {
        link.classList.remove('active');
      }
    });
  };

  // Run the updateActiveClass function on component mount
  onMount(() => {
    updateActiveClass();
  });
</script>
  
  <style>
    main {
      font-family: sans-serif;
    }
  
    .menu {
      position: fixed;
      background: white;
      left: 0;
      top: 0;
      bottom: 0;
      overflow: hidden;
      width: 80px;
      transition: 300ms;
    }
  
    .menu.active {
      width: 400px;
    }
  
    .menu.active .menu__Link {
      color: black;
    }
  
    .menu__List {
      all: unset;
      display: block;
      width: 100%;
    }
  
    .menu__Item {
      display: block;
    }
  
    .menu__Link {
      display: block;
      padding: 5px;
      margin: 15px;
      text-decoration: none;
      white-space: nowrap;
      border-radius: 30px;
      color: transparent;
      transition: 300ms;
    }
  
    .menu__Link:hover {
      color: orange;
    }
  
    .menu__Link.active {
      background: #555;
    }
  
    .menu__Link::before {
      content: attr(title);
      display: inline-block;
      width: 40px;
      height: 40px;
      line-height: 40px;
      text-align: center;
      margin-right: 20px;
      color: orange;
    }
  
    .menu__Toggle {
      all: unset;
      font-size: 14px;
      color: black;
      padding: 15px;
      font-weight: bold;
      background: #fff;
      margin: 10px;
      cursor: pointer;
    }
  
    .wrapper {
      margin-left: 80px;
      padding-left: 40px;
      transition: 300ms;
    }
  
    .wrapper.active {
      margin-left: 400px;
    }
  </style>
  
  <main>
    <nav class="menu" class:active="{ navActive }" >
      <button class="menu__Toggle" on:click={() => toggleNav()}>
        {#if navActive}
          <CloseOutline/>
        {:else}
          <!-- You can replace 'X' with another icon if you have a specific one for closing -->
          <HomeSolid/>
        {/if}
      </button>
      <!-- <button class="menu__Toggle" on:click="{ () => toggleNav() }">{ navActive ? 'X' : '>'}</button> -->
      <ul class="menu__List">
        <li class="menu__Item"><a title="🐶"  class="menu__Link active" href="/transactions">Transactions</a></li>
        <li class="menu__Item"><a title="🐶" class="menu__Link" href="/customers">Customers</a></li>
        <li class="menu__Item"><a title="🙈" class="menu__Link" href="/payhistoryview">Payment History</a></li>
        <li class="menu__Item"><a title="🐻" class="menu__Link" href="/widgets">Widgets</a></li>
      </ul>
    </nav>
      <div class="wrapper" class:active="{ navActive }"></div>
  </main>