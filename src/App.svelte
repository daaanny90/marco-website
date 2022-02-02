<script>
  import Navbar from "./components/Navbar.svelte"
  import {Route, router} from 'tinro'; 
  import Home from "./pages/Home.svelte"
  import About from "./pages/About.svelte"
  import Contacts from "./pages/Contacts.svelte"

  router.mode.hash();
</script>

<Navbar />
<main>
  <Route path="/"><Home /></Route>
  <Route path="/about"><About /></Route>
  <Route path="/contacts"><Contacts /></Route>
</main>

<style lang="scss">

</style>
