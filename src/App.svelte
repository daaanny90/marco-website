<script>
  import Navbar from "./components/Navbar.svelte";
  import { Route, router, meta } from "tinro";
  import Home from "./pages/Home.svelte";
  import About from "./pages/About.svelte";
  import Contacts from "./pages/Contacts.svelte";
  import Transition from "./components/Transition.svelte";
  import NotFound from "./pages/404.svelte";

  router.mode.hash();
</script>

<Navbar />
<main>
  <Transition>
    <Route>
      <Route path="/"><Home /></Route>
      <Route path="/about"><About /></Route>
      <Route path="/contacts"><Contacts /></Route>
      <Route fallback><NotFound/></Route>
    </Route>
  </Transition>
</main>

<style lang="scss">
</style>
