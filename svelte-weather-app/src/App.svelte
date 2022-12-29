<script lang="ts">
  import './tailwind.css';
  import { Router, Link, Route } from "svelte-routing";
  import Home from './routes/Home.svelte';
  import Inflation from './routes/Inflation.svelte';
  
  export let url = "";
</script>

<Router url="{url}">
  <div class="h-screen grid grid-rows-[auto_1fr] bg-white text-slate-800 dark:bg-slate-800 dark:text-white">
    <nav class="flex justify-between p-4">
      <span>Svelte inflation info app</span>

      <div>
        <Link to="/" class="p-2 rounded-lg transition hover:bg-slate-100 dark:hover:bg-slate-700">Home</Link>
        <Link to="inflation" class="p-2 rounded-lg transition hover:bg-slate-100 dark:hover:bg-slate-700">Inflation info</Link>
      </div>
    </nav>
    
    <main class="grid place-items-center">
      <Route path="inflation" component="{Inflation}" />
      <Route path="/" component="{Home}" />
    </main>
  </div>
</Router>