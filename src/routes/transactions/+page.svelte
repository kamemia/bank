<script>
    import TransactionsCard from "$lib/components/Cards/TransactionsCard.svelte";
    import { InlineCalendar } from 'svelte-calendar';
    
    const theme = {
		calendar: {
			width: '300px',
            maxWidth: '100vw',
            legend: {
                height: '35px'
            },
            font:{
                regular:"1.0em"
            },
			shadow: '0px 0px 5px rgba(0, 0, 0, 0.25)'
		}
	};
    
</script>

<div class="flex items-center">
    <div class="pt-24 pb-12"><TransactionsCard /></div>
</div>
<div class="mb-4 mr-2 absolute bottom-0 right-0">
<InlineCalendar {theme}/>
</div>