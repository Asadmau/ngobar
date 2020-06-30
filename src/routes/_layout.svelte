<script>
  //   import Nav from "../components/Nav.svelte";
  //   import Navbar from "../components/Navbar";
  import Sidbar from "../components/sidbar.svelte";
  import Navbar from "../components/Navbar.svelte";
  export let segment;
</script>

<style>

</style>

<Sidbar {segment} />

<!-- <Nav {segment} /> -->

<!-- <div class="main-content" id="panel"> -->
<div class="main-content" id="panel">
  <Navbar />
  <slot />
</div>
<!-- </div> -->
