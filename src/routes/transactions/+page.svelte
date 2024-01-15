<script>
    import TransactionsCard from "$lib/components/Cards/TransactionsCard.svelte";
    import { InlineCalendar } from 'svelte-calendar';
    
    const theme = {
		calendar: {
			width: '400px',
			shadow: '0px 0px 5px rgba(0, 0, 0, 0.25)'
		}
	};
    
</script>

<div class="flex items-center">
    <div class="pt-24 pb-12"><TransactionsCard /></div>
</div>

<InlineCalendar {theme}/>