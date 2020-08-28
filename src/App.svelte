<script>
  import MainContent from "./component/MainContent.svelte";
  import Navbar from "./component/Navbar.svelte";
  import SearchBar from "./component/SearchBar.svelte";
</script>

<div class="row">
  <div class="col">
    <Navbar />
  </div>
</div>
<div class="row my-3">
  <div class="col">
    <SearchBar keyword="" />
  </div>
</div>
<!-- <div class="row">
  <div class="col">
    <MainContent />
  </div>
</div> -->
