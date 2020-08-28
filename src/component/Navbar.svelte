<script>
  let list = "list 1";
</script>

<style>

</style>

<nav class="navbar navbar-expand-lg navbar-dark bg-dark">
  <div class="container">
    <a class="navbar-brand" href="#">Julpin Movie</a>
    <button
      class="navbar-toggler"
      type="button"
      data-toggle="collapse"
      data-target="#navbarSupportedContent"
      aria-controls="navbarSupportedContent"
      aria-expanded="false"
      aria-label="Toggle navigation">
      <span class="navbar-toggler-icon" />
    </button>

    <div class="collapse navbar-collapse" id="navbarSupportedContent">
      <ul class="navbar-nav mr-auto">
        <li class:active={list === 'list 1'} class="nav-item active">
          <a
            class="nav-link"
            href="#"
            on:click={() => {
              list = 'list 1';
            }}>
            Home
          </a>
        </li>

      </ul>
    </div>
  </div>
</nav>
