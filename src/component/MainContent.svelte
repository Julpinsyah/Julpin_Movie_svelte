<script>
  import { dataset_dev } from "svelte/internal";

  export let keyword;
  let id = 0;

  let promise = getMovies();

  async function getMovies(m) {
    return fetch("http://www.omdbapi.com/?apikey=807a3da6&s=" + m)
      .then((Response) => {
        if (!Response.ok) {
          throw new Error(Response.statusText);
        }

        return Response.json();
      })
      .then((Response) => {
        if (Response.Response === "False") {
          throw new Error(Response.Error);
        }
        return Response.Search;
      });
  }

  async function getDetail(data) {
    return fetch(
      "http://www.omdbapi.com/?apikey=807a3da6&i=" + data
    ).then((Response) => Response.json());
  }

  let promise2 = getDetail(id);

  $: if (keyword.length > 2) {
    console.log(keyword);
    promise = getMovies(keyword);
    console.log(promise);
  }
</script>

<div class="container">
  <div class="row">
    {#if keyword == ''}
      <table class="table">
        <thead>
          <tr>
            <th scope="col" class="text-center">Masukkan Pencarian Anda</th>
          </tr>
        </thead>
      </table>
    {:else}
      {#await promise}
        <div class="d-flex justify-content-center">
          <div
            class="spinner-border text-primary spinner-border-xl"
            role="status">
            <span class="sr-only">Loading...</span>
          </div>
        </div>
      {:then data}
        {#each data as d}
          <div class="col col-md-3 mb-3">
            <div class="card h-100">
              <img src={d.Poster} class="card-img-top" alt="..." />
              <div class="card-body">
                <h5 class="card-title">{d.Title}</h5>
                <p class="card-text">
                  <small class="text-muted">{d.Year}</small>
                </p>
                <div
                  class="card-footer text-center"
                  style="border-top-width: 0px;background-color: #fff">
                  <button
                    class="btn btn-primary"
                    data-toggle="modal"
                    data-target="#exampleModal"
                    on:click={() => {
                      id = d.imdbID;
                      promise2 = getDetail(id);
                    }}>
                    Detail
                  </button>
                </div>
              </div>
            </div>
          </div>
        {/each}
      {:catch error}
        <table class="table">
          <thead>
            <tr>
              <th scope="col" class="text-center">{error.message}</th>
            </tr>
          </thead>
        </table>
      {/await}
    {/if}
  </div>

</div>

<!-- Modal -->
<div
  class="modal fade"
  id="exampleModal"
  tabindex="-1"
  aria-labelledby="exampleModalLabel"
  aria-hidden="true">
  <div class="modal-dialog modal-dialog-centered modal-lg">
    <div class="modal-content">
      <div class="modal-header bg-primary text-light">
        <h5 class="modal-title" id="exampleModalLabel">Modal title</h5>
        <button
          type="button"
          class="close"
          data-dismiss="modal"
          aria-label="Close">
          <span aria-hidden="true">&times;</span>
        </button>
      </div>
      <div class="modal-body">
        {#await promise2}
          <div class="d-flex justify-content-center">
            <div
              class="spinner-border text-primary spinner-border-xl"
              role="status">
              <span class="sr-only">Loading...</span>
            </div>
          </div>
        {:then dt}
          <div class="card border-light">
            <div class="row no-gutters">
              <div class="col-md-3 pt-2">
                <img
                  src={dt.Poster}
                  class="card-img img-fluid mt-2"
                  alt="..." />
              </div>
              <div class="col-md-9">
                <div class="card-body pt-0">
                  <ul class="list-group list-group-flush">
                    <li class="list-group-item">
                      <h2>{dt.Title}({dt.Year})</h2>
                    </li>
                    <li class="list-group-item">
                      <strong>Duration :</strong>
                      {dt.Runtime}
                    </li>
                    <li class="list-group-item">
                      <strong>Director :</strong>
                      {dt.Director}
                    </li>
                    <li class="list-group-item">
                      <strong>Actors :</strong>
                      <br />
                      {dt.Actors}
                    </li>
                    <li class="list-group-item">
                      <strong>Synopsis :</strong>
                      <br />
                      {dt.Plot}
                    </li>
                  </ul>
                </div>
              </div>
            </div>
          </div>
        {:catch error}
          <p style="color: red">{error.message}</p>
        {/await}
      </div>
      <div class="modal-footer">
        <button type="button" class="btn btn-secondary" data-dismiss="modal">
          Close
        </button>
      </div>
    </div>
  </div>
</div>
