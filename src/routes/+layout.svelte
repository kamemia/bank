<script lang="ts">
    import '../app.css';
    import Menu from '../lib/components/Menu/Menu.svelte';
    import PersonsCard from '$lib/components/Cards/PersonsCard.svelte';
</script>

<div class="flex px-4 mx-auto w-full">
    <main class="lg:ml-72 w-full mx-auto">
      <slot />
      <Menu />
    </main>
</div>

