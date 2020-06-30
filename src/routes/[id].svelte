<script context="module">
  // export async function preload({ query, params }) {
  //   console.log(params.id);
  //   if (params.id == "createMahasiswa") {
  //     //   add = true;
  //     return { add: true };
  //   }
  //   const data = await fetch(
  //     `http://localhost:5000/mahasiswa/${params.id}`
  //   ).then(res => res.json());
  //   console.log(data);
  //   return { mahasiswa: data };
  // }

  //fetch backand or ambil data backand
  export async function preload({ query, params }) {
    console.log("sukses", params);
    if (params.id == "createMahasiswa") {
      return { add: true };
    }

    const data = await fetch(
      `http://localhost:5000/mahasiswa/${params.id}`
    ).then(res => res.json());
    return { mahasiswa: data, id: params.id };

    // const data = await fetch(`http://localhost:5000/mahasiswa/${params.id}`);
    // const mhs = data.json();
    // return { mahasiswa: mhs };
  }
</script>

<script>
  // import le
  import { onMount } from "svelte";
  import { goto } from "@sapper/app";
  export let mahasiswa;
  export let add;
  export let id;
  let username = "";
  let email = "";
  let password = "";
  let alamat = "";
  let tgl_lahir = "";
  let create_at = "";
  let hoby = [];
  let condisionalHoby = false;
  let isiHoby = "";
  onMount(() => {
    if (mahasiswa) {
      username = mahasiswa.username;
      email = mahasiswa.email;
      password = mahasiswa.password;
      alamat = mahasiswa.alamat;
      tgl_lahir = mahasiswa.tgl_lahir;
      hoby = mahasiswa.hoby;
      create_at = convertDate(mahasiswa.created_at);
    }
  });
  const convertDate = isoDate => {
    var d = new Date(isoDate);
    return (
      d.toLocaleDateString() +
      " " +
      d.toTimeString().substring(0, d.toTimeString().indexOf("GMT"))
    );
  };
  const displayInput = () => {
    condisionalHoby = true;
  };
  const addHobby = () => {
    hoby = [...hoby, isiHoby];
    isiHoby = "";
    condisionalHoby = false;
    console.log(hoby);
  };
  const onKeyPress = e => {
    if (e.charCode === 13) addHobby();
  };
  let deleteHobby = i => {
    // delete hobby[hobby.indexOf(i)];
    // hobby = [...hobby.slice(i,i)];
    hoby = hoby.filter((x, id) => id !== i);
    console.log(hoby);
  };

  //fetch data rest api
  const postData = async () => {
    await fetch(`http://localhost:5000/mahasiswa`, {
      method: "POST",
      headers: { "Content-Type": "application/json" },
      body: JSON.stringify({
        username,
        email,
        password,
        alamat,
        tgl_lahir,
        hoby
      })
      // body: {
      //   username: username,
      //   email: email,
      //   password: password,
      //   alamat: alamat,
      //   tgl_lahir: tgl_lahir,
      //   hoby: hoby
      // }
    })
      .then(result => {
        console.log(result);
        goto("/");
      })
      .catch(r => {
        console.log(r);
      });
  };

  //fecth edit data method
  const pacthData = async () => {
    await fetch(`http://localhost:5000/mahasiswa/${id}`, {
      method: "PATCH",
      headers: { "Content-Type": "application/json" },
      body: JSON.stringify({
        username,
        email,
        password,
        alamat,
        tgl_lahir,
        hoby
      })
      // body: {
      //   username: username,
      //   email: email,
      //   password: password,
      //   alamat: alamat,
      //   tgl_lahir: tgl_lahir,
      //   hoby: hoby
      // }
    })
      .then(result => {
        console.log(result);
        goto("/");
      })
      .catch(r => {
        console.log(r);
      });
  };

  //Fecth delete data
  const deleteData = async () => {
    if (confirm("hapus data" + username)) {
      await fetch(`http://localhost:5000/mahasiswa/${id}`, {
        method: "DELETE"
      })
        .then(result => {
          console.log(result);
          goto("/");
        })
        .catch(r => {
          console.log(r);
        });
    }
  };
</script>

<div class="col-xl-8 order-xl-1 mt-3">
  <div class="card">
    <div class="card-header">
      <div class="row align-items-center">
        <div class="col-8">
          {#if add}
            <h3 class="mb-0">Tambah Data</h3>
          {:else}
            <h3 class="mb-0">Edit Data</h3>
            <p>Created At : {create_at}</p>
          {/if}
        </div>
        <div class="col-4 text-right">
          {#if add}
            <button on:click={postData} class="btn btn-sm btn-primary">
              Buat Mhs
            </button>
          {:else}
            <button on:click={deleteData} class="btn btn-sm btn-danger">
              DELETE
            </button>
            <button on:click={pacthData} class="btn btn-sm btn-success">
              Update Mhs
            </button>
          {/if}
        </div>
      </div>
    </div>
    <div class="card-body">
      <div>
        <h6 class="heading-small text-muted mb-4">User information</h6>
        <div class="pl-lg-4">
          <div class="row">
            <div class="col-lg-6">
              <div class="form-group">
                <label class="form-control-label" for="input-username">
                  Username
                </label>
                <input
                  type="text"
                  id="input-username"
                  class="form-control"
                  placeholder="Username"
                  bind:value={username} />
              </div>
            </div>
            <div class="col-lg-6">
              <div class="form-group">
                <label class="form-control-label" for="input-email">
                  Email address
                </label>
                <input
                  type="email"
                  id="input-email"
                  class="form-control"
                  placeholder="Andyceng11@example.com"
                  bind:value={email} />
              </div>
            </div>
          </div>
          <div class="row">
            <div class="col-lg-6">
              <div class="form-group">
                <label class="form-control-label" for="input-first-name">
                  Password
                </label>
                <input
                  type="password"
                  id="input-first-name"
                  class="form-control"
                  placeholder="Password"
                  bind:value={password} />
              </div>
            </div>
            <div class="col-lg-6">
              <div class="form-group">
                <label class="form-control-label" for="input-last-name">
                  Tanggal Lahir
                </label>
                <input
                  type="text"
                  id="input-last-name"
                  class="form-control"
                  placeholder="Tanggal Lahir"
                  bind:value={tgl_lahir} />
              </div>
            </div>
          </div>
        </div>
        <hr class="my-4" />
        <!-- Address -->
        <h6 class="heading-small text-muted mb-4">Mahasiswa information</h6>
        <div class="pl-lg-4">
          <div class="row">
            <div class="col-md-12">
              <div class="form-group">
                <label class="form-control-label" for="input-address">
                  Address
                </label>
                <input
                  id="input-address"
                  class="form-control"
                  placeholder="Home Address"
                  bind:value={alamat}
                  type="text" />
              </div>
            </div>
          </div>
          <div class="">
            <div class="col-md-6">
              <div class="card">
                <div class="card-header border-0">
                  <div class="row align-items-center">

                    {#if condisionalHoby}
                      <div class="input-group input-group-sm mb-3">
                        <input
                          type="text"
                          class="form-control"
                          placeholder="Tuliskan hobby"
                          aria-label="Tuliskan hobby"
                          bind:value={isiHoby}
                          on:keypress={onKeyPress} />
                        <div class="input-group-append">
                          <button
                            class="btn btn-outline-primary"
                            type="button"
                            on:click={addHobby}>
                            Add Hoby
                          </button>
                        </div>
                      </div>
                    {:else}
                      <div class="col">
                        <h3 class="mb-0">Hobby</h3>
                      </div>
                      <div class="col text-right">
                        {#if add}
                          <button
                            class="btn btn-sm btn-primary"
                            on:click={displayInput}>
                            Tambah
                          </button>
                        {:else}
                          <button
                            class="btn btn-sm btn-primary"
                            data-toggle="modal"
                            data-target="#modal-notification">
                            Ubah
                          </button>
                        {/if}
                      </div>
                    {/if}

                  </div>
                </div>
                <div class="table-responsive">
                  <!-- Projects table -->
                  <table class="table align-items-center table-flush">
                    <tbody>
                      {#each hoby as item, i}
                        <tr>
                          <td>{item}</td>
                          <td>
                            <button
                              class="btn btn-danger btn-sm"
                              on:click={() => deleteHobby(i)}>
                              <i class="ni ni-fat-delete" />
                            </button>
                          </td>
                        </tr>
                      {/each}

                    </tbody>
                  </table>
                </div>
              </div>
            </div>
            <!-- <div class="col-lg-4">
              <div class="form-group">
                <label class="form-control-label" for="input-city">City</label>
                <input
                  type="text"
                  id="input-city"
                  class="form-control"
                  placeholder="City"
                  value="New York" />
              </div>
            </div>
            <div class="col-lg-4">
              <div class="form-group">
                <label class="form-control-label" for="input-country">
                  Country
                </label>
                <input
                  type="text"
                  id="input-country"
                  class="form-control"
                  placeholder="Country"
                  value="United States" />
              </div>
            </div>
            <div class="col-lg-4">
              <div class="form-group">
                <label class="form-control-label" for="input-country">
                  Postal code
                </label>
                <input
                  type="number"
                  id="input-postal-code"
                  class="form-control"
                  placeholder="Postal code" />
              </div>
            </div> -->
          </div>
        </div>
      </div>
    </div>
  </div>
</div>

<div class="col-md-4">
  <div
    class="modal fade"
    id="modal-notification"
    tabindex="-1"
    role="dialog"
    aria-labelledby="modal-notification"
    aria-hidden="true">
    <div
      class="modal-dialog modal-danger modal-dialog-centered modal-"
      role="document">
      <div class="modal-content bg-gradient-danger">

        <div class="modal-header">
          <h6 class="modal-title" id="modal-title-notification">Input hoby</h6>
          <button
            type="button"
            class="close"
            data-dismiss="modal"
            aria-label="Close">
            <span aria-hidden="true">×</span>
          </button>
        </div>

        <div class="modal-body">

          <div class="py-3 text-center" />
          <div class="input-group input-group-sm mb-3">
            <input
              type="text"
              class="form-control"
              placeholder="Tuliskan hobby"
              aria-label="Tuliskan hobby"
              bind:value={isiHoby}
              on:keypress={onKeyPress} />
            <div class="input-group-append">
              <button
                class="btn btn-dark"
                data-dismiss="modal"
                type="button"
                on:click={addHobby}>
                Add Hoby
              </button>
            </div>
          </div>

        </div>

        <div class="modal-footer">
          <button type="button" class="btn btn-white">Ok, Got it</button>
          <button type="button" class="btn btn-link text-white ml-auto">
            Close
          </button>
        </div>

      </div>
    </div>
  </div>
</div>
