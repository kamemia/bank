<script lang="ts">
    import '../app.css';
    import Navbar from '$lib/components/Navbar/Navbar.svelte';
</script>

<div class="flex px-4 mx-auto w-full ">
    <main class="lg:ml-72 w-full mx-auto">
      <Navbar/>
      <slot />
    </main>
</div>


