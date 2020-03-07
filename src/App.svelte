<script>
  import { Router, Route } from "yrv";

  import Index from "./pages/Index.svelte";
</script>

{#if location.hostname !== "localhost"}
    <base href="foodtime/">
{/if}


<Router>
  <Route exact component={Index} />
  <Route exact path="#" component={Index} />
</Router>

