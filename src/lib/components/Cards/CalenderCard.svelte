<script>
    import { InlineCalendar } from 'svelte-calendar';
    import PersonsCard from './PersonsCard.svelte';

    const theme = {
		calendar: {
			width: '270px',
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
<style>
    .spacer{
        height: 15px;
    }
</style>

<div class="w-full max-w-xs p-4 bg-white  rounded-lg  dark:bg-gray-800 dark:border-gray-700">
    <PersonsCard/>
    <div class="spacer"></div>
    <div class="w-full max-w-xs">
        <InlineCalendar {theme}/>
    </div>
</div>
