<script>
  import { Router, Route } from "yrv";

  import Index from "./pages/Index.svelte";
</script>

<Router>
  <Route exact component={Index} />
  <Route exact path="#" component={Index} />
  <Route fallback>Not found</Route>
</Router>
