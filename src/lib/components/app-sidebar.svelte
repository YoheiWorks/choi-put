<script lang="ts">
 import CalendarIcon from "@lucide/svelte/icons/calendar";
 import LayoutDashboard from "@lucide/svelte/icons/layout-dashboard"
 import InboxIcon from "@lucide/svelte/icons/inbox";
 import SearchIcon from "@lucide/svelte/icons/search";
 import SettingsIcon from "@lucide/svelte/icons/settings";
 import * as Sidebar from "$lib/components/ui/sidebar/index.js";
 
 // Menu items.
 const items = [
  {
   title: "ダッシュボード",
   url: "#",
   icon: LayoutDashboard,
  },
  {
   title: "Inbox",
   url: "#",
   icon: InboxIcon,
  },
  {
   title: "Calendar",
   url: "#",
   icon: CalendarIcon,
  },
  {
   title: "Search",
   url: "#",
   icon: SearchIcon,
  },
  {
   title: "Settings",
   url: "#",
   icon: SettingsIcon,
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