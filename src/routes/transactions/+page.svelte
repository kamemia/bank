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

<div class="flex">
    <Menu />
    <!-- Left-aligned TransactionsCard -->
    <div class="pt-24 pb-12 pr-4">
        <TransactionsCard />
    </div>

    <!-- Container for PersonsCard and Calendar -->
    <div class="flex flex-col items-end">
        <!-- Right-aligned PersonsCard -->
        <div class="pt-24 pr-4">
            <PersonsCard />
        </div>

        <!-- Calendar positioned under PersonsCard -->
        <div class="mb-4 mr-2">
            <InlineCalendar {theme} />
        </div>
    </div>
</div>