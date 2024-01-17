<script>
    import TransactionsCard from "$lib/components/Cards/TransactionsCard.svelte";
    import { InlineCalendar } from 'svelte-calendar';
    import PersonsCard from "$lib/components/Cards/PersonsCard.svelte";
    import Menu from '$lib/components/Menu/Menu.svelte'

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

<div class="grid grid-flow-col grid-rows-3 gap-4">
    <Menu />
    <!-- Left-aligned TransactionsCard -->
    <div class="row-span-3">
        <TransactionsCard />
    </div>

    <!-- Container for PersonsCard and Calendar -->
    
        <!-- Right-aligned PersonsCard -->
        <div class="col-span-2">
            <PersonsCard />
        </div>

        <!-- Calendar positioned under PersonsCard -->
        <div class="col-span-2 row-span-2">
            <InlineCalendar {theme} />
        </div>
    
</div>