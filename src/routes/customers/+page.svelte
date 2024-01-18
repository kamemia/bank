<script src="../path/to/flowbite/dist/datepicker.js">

    import Menu from '$lib/components/Menu/Menu.svelte';
    import Tab1 from '$lib/components/Tabs/Tab.svelte';
    import Tab2 from '$lib/components/Tabs/Tab1.svelte';
    import Tab3 from '$lib/components/Tabs/Tab2.svelte';
    import Tabs from '$lib/components/Tabs/Tabs.svelte';
    import PersonsCard from '$lib/components/Cards/PersonsCard.svelte';

    let items = [
        {
            label: "Information",
            value: 1,
            component: Tab1
        },
        {
            label: "Payment History",
            value: 2,
            component: Tab2
        },
        {
            label: "Statistics",
            value: 3,
            component: Tab3
        }
    ];
</script>


<Menu/>
<div class="grid grid-cols-5 grid-rows-5 gap-4">
   
    <div class="col-span-4 row-span-5">
        <Tabs {items}/>
    </div>
    <div class="row-span-5 col-start-5"><PersonsCard/></div>
</div>