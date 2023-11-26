<script>
  import { Router, Link, Route } from "svelte-routing";

  import Home from "../routes/Home.svelte";
  import Detail from "../routes/Detail.svelte";

  import "primer/css/core/index.scss";

  export let url = "";
</script>

<Router {url}>
  <div class="container">
    <header class="masthead">
      <h1 class="site-title">
        <Link to="/">Pokédex</Link>
      </h1>
    </header>

    <main>
      <Route path="/:id" component={Detail} />
      <Route path="/" component={Home} />
    </main>
  </div>
</Router>

<style>
  .container {
    max-width: 36rem;
    margin: 0 auto;
  }

  .masthead {
    padding-bottom: 0.5rem;
    margin-bottom: 3rem;
    border-bottom: 0.125rem solid var(--color-details);
  }
</style>
