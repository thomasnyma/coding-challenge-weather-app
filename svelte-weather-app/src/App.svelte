<script lang="ts">
  import './tailwind.css';
  
  import { Router, Link, Route } from "svelte-routing";
  import Home from './routes/Home.svelte';
  import Weather from './routes/Weather.svelte';
  
  export let url = "";
</script>

<Router url="{url}">
  <nav>
    <Link to="/">Home</Link>
    <Link to="weather">Weather</Link>
  </nav>
  <main>
    <Route path="weather" component="{Weather}" />
    <Route path="/" component="{Home}" />
  </main>
</Router>