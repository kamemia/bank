<script src="../path/to/flowbite/dist/datepicker.js">

    import Menu from '$lib/components/Menu/Menu.svelte';
    import Tab1 from '$lib/components/Tabs/Tab.svelte';
    import Tab2 from '$lib/components/Tabs/Tab1.svelte';
    import Tab3 from '$lib/components/Tabs/Tab2.svelte';
    import Tabs from '$lib/components/Tabs/Tabs.svelte';

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

<div>
    <Tabs {items}/>
</div>