<script lang="ts">
    import TabBar from '$lib/components/navigation/NavigationMenu.svelte';
    import type { PageServerData } from '../../../routes/$types';

    // Props
    let { data }: { data: PageServerData['destinations'] } = $props();

    // Local variables
    const tabBarSections = data.map((destination) => destination.name);

    // States
    let activeTabBarItemIndex = $state(0);

    // Event listeners
    const onTabBarItemClick = (index: number) => (activeTabBarItemIndex = index);
</script>

<div id="destination">
    <TabBar
        sections={tabBarSections}
        activeIndex={activeTabBarItemIndex}
        usePrefixes={false}
        displayBackground={false}
        onItemClick={onTabBarItemClick}
        --height="36px"
        --padding="0"
        --colorOfInactiveItems="var(--light-blue)"
    />
</div>

<style>
    #destination {
        height: 100vh;
        background-image: url('images/destination/background-destination-desktop.jpg');
        background-size: cover;
        background-repeat: no-repeat;
    }
</style>
