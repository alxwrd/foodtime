<script>
  import { Router, Route } from "yrv";

  import Index from "./pages/Index.svelte";
</script>

<Router>
  <Route exact component={Index} />
  <Route fallback>Not Found</Route>
  <Route exact path="#" component={Index} />
</Router>
