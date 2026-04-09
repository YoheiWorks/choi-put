<script lang="ts">
 import LibraryIcon from "@lucide/svelte/icons/library-big";
 import LayoutDashboardIcon from "@lucide/svelte/icons/layout-dashboard"
 import MapIcon from "@lucide/svelte/icons/map";
 import * as Sidebar from "$lib/components/ui/sidebar/index.js";
 
 // Menu items.
 const items = [
  {
   title: "ダッシュボード",
   url: "#",
   icon: LayoutDashboardIcon,
  },
  {
   title: "クエスト",
   url: "#",
   icon: MapIcon,
  },
  {
   title: "ナレッジ",
   url: "#",
   icon: LibraryIcon,
  },
 ];
</script>
 
<Sidebar.Root collapsible='icon'>
 <Sidebar.Content>
  <Sidebar.Group>
   <!-- <Sidebar.GroupLabel>choi-put</Sidebar.GroupLabel> -->
   <Sidebar.GroupContent>
    <Sidebar.Menu>
     {#each items as item (item.title)}
      <Sidebar.MenuItem>
       <Sidebar.MenuButton>
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