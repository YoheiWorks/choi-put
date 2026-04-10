<script lang="ts">
    import { page } from '$app/state';
    import LibraryIcon from "@lucide/svelte/icons/library-big";
    import LayoutDashboardIcon from "@lucide/svelte/icons/layout-dashboard"
    import MapIcon from "@lucide/svelte/icons/map";
    import * as Sidebar from "$lib/components/ui/sidebar/index.js";
 
    // Menu items.
    const items = [
    {
        title: "ダッシュボード",
        url: "/",
        icon: LayoutDashboardIcon,
    },
    {
        title: "クエスト",
        url: "/quests",
        icon: MapIcon,
    },
    {
        title: "ナレッジ",
        url: "/knowledge",
        icon: LibraryIcon,
    },
    ];
</script>
 
<Sidebar.Root collapsible='icon'>
    <Sidebar.Content>
        <Sidebar.Group>
            <Sidebar.GroupContent>
                <Sidebar.Menu>
                    <Sidebar.Trigger />
     {#each items as item (item.title)}
      <Sidebar.MenuItem>
       <Sidebar.MenuButton isActive={page.url.pathname === item.url}>
        {#snippet child({ props })}
         <a href={item.url} {...props}>
          <item.icon />
          <span>{item.title}</span>
         </a>
        {/snippet}
       </Sidebar.MenuButton>
      </Sidebar.MenuItem>
     {/each}
    </Sidebar.Menu>
   </Sidebar.GroupContent>
  </Sidebar.Group>
 </Sidebar.Content>
</Sidebar.Root>