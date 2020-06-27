<script>
  import { onMount } from "svelte";
  import Global from "./Global.svelte";
  import Country from "./Country.svelte";
  import State from "./State.svelte";
  import Menu from "./components/Menu.svelte";
</script>

<main>
  <Menu />
  <div class="container mt-5">
	<Global />
  <!-- <State /> -->
  <Country />
  </div>
  
</main>
