<script lang="ts">
    import TransactionsTable from '$lib/components/Cards/TransactionsTable.svelte';
    import { InlineCalendar } from 'svelte-calendar';
    import PersonsCard from "$lib/components/Cards/PersonsCard.svelte";
    import Menu from '$lib/components/Menu/Menu.svelte'
    // import FullCalendar, { type CalendarOptions } from 'svelte-fullcalendar';
    // import daygridPlugin from '@fullcalendar/daygrid';

    // let options: CalendarOptions = {
    //     initialView: 'dayGridMonth',
    //     plugins: [daygridPlugin]
    // };

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


<Menu/>
<div class="grid grid-cols-5 grid-rows-5 gap-4">
    
    <div class="col-span-4 row-span-5"><TransactionsTable/></div>
    <div class="row-span-4 col-start-5"><PersonsCard/></div>
    
    <div class="col-start-5 row-start-5"><InlineCalendar {theme}/></div>
</div>
    