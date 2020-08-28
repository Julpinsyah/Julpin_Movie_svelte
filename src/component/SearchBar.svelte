<script>
  import MainContent from "./MainContent.svelte";

  export let keyword;
  let kunci = "";

  function isidata() {
    kunci = keyword;
  }

  // $: console.log(keyword);
</script>

<div class="container">
  <div class="input-group my-4 mx-auto col-md-8">
    <input
      id="inputCari"
      type="text"
      class="form-control"
      placeholder="keyword..."
      bind:value={keyword}
      on:keypress={(e) => {
        if (e.keyCode == 13) {
          isidata();
        }
      }} />
    <div class="input-group-append">
      <button class="btn btn-primary" on:click={isidata}>🔎 Cari</button>
    </div>
  </div>
</div>
<MainContent keyword={kunci} />
