<script>
  import { onMount } from "svelte";
  import { goto } from "@sapper/app";

  let data = [];
  onMount(() => {
    getData();
  });

  const getData = async () => {
    await fetch("http://localhost:5000/mahasiswa")
      .then(result => {
        return result.json();
      })
      .then(mhs => {
        data = mhs;
        console.log(data);
      })
      .catch(err => {
        console.log(err);
      });
  };

  const TambahData = () => {
    goto("/createMahasiswa");
  };
</script>

<svelte:head>
  <title>Sapper project template</title>
</svelte:head>

<!-- Main content -->

<!-- Header -->
<div class="header bg-primary pb-6">
  <div class="container-fluid">
    <div class="header-body">
      <div class="row align-items-center py-4">
        <div class="col-lg-6 col-7">
          <h6 class="h2 text-white d-inline-block mb-0">Default</h6>
          <nav aria-label="breadcrumb" class="d-none d-md-inline-block ml-md-4">
            <ol class="breadcrumb breadcrumb-links breadcrumb-dark">
              <li class="breadcrumb-item">
                <a href=".">
                  <i class="fas fa-home" />
                </a>
              </li>
              <li class="breadcrumb-item">
                <a href="\\" activlink>Dosen</a>
              </li>
            </ol>
          </nav>
        </div>
        <div class="col-lg-6 col-5 text-right">
          <a href="." class="btn btn-sm btn-neutral">New</a>
          <a href="." class="btn btn-sm btn-neutral">Filters</a>
        </div>
      </div>
      <!-- Card stats -->
      <div class="row">
        <div class="col-xl-3 col-md-6">
          <div class="card card-stats">
            <!-- Card body -->
            <div class="card-body">
              <div class="row">
                <div class="col">
                  <h5 class="card-title text-uppercase text-muted mb-0">
                    Mahasiswa
                  </h5>
                  <span class="h2 font-weight-bold mb-0">{data.length}</span>
                </div>
                <div class="col-auto">
                  <div
                    class="icon icon-shape bg-gradient-red text-white
                    rounded-circle shadow">
                    <i class="ni ni-active-40" />
                  </div>
                </div>
              </div>
              <p class="mt-3 mb-0 text-sm">
                <span class="text-success mr-2">
                  <i class="fa fa-arrow-up" />
                  3.48%
                </span>
                <span class="text-nowrap">Since last month</span>
              </p>
            </div>
          </div>
        </div>
        <div class="col-xl-3 col-md-6">
          <div class="card card-stats">
            <!-- Card body -->
            <div class="card-body">
              <div class="row">
                <div class="col">
                  <h5 class="card-title text-uppercase text-muted mb-0">
                    New users
                  </h5>
                  <span class="h2 font-weight-bold mb-0">2,356</span>
                </div>
                <div class="col-auto">
                  <div
                    class="icon icon-shape bg-gradient-orange text-white
                    rounded-circle shadow">
                    <i class="ni ni-chart-pie-35" />
                  </div>
                </div>
              </div>
              <p class="mt-3 mb-0 text-sm">
                <span class="text-success mr-2">
                  <i class="fa fa-arrow-up" />
                  3.48%
                </span>
                <span class="text-nowrap">Since last month</span>
              </p>
            </div>
          </div>
        </div>
        <div class="col-xl-3 col-md-6">
          <div class="card card-stats">
            <!-- Card body -->
            <div class="card-body">
              <div class="row">
                <div class="col">
                  <h5 class="card-title text-uppercase text-muted mb-0">
                    Sales
                  </h5>
                  <span class="h2 font-weight-bold mb-0">924</span>
                </div>
                <div class="col-auto">
                  <div
                    class="icon icon-shape bg-gradient-green text-white
                    rounded-circle shadow">
                    <i class="ni ni-money-coins" />
                  </div>
                </div>
              </div>
              <p class="mt-3 mb-0 text-sm">
                <span class="text-success mr-2">
                  <i class="fa fa-arrow-up" />
                  3.48%
                </span>
                <span class="text-nowrap">Since last month</span>
              </p>
            </div>
          </div>
        </div>
        <div class="col-xl-3 col-md-6">
          <div class="card card-stats">
            <!-- Card body -->
            <div class="card-body">
              <div class="row">
                <div class="col">
                  <h5 class="card-title text-uppercase text-muted mb-0">
                    Performance
                  </h5>
                  <span class="h2 font-weight-bold mb-0">49,65%</span>
                </div>
                <div class="col-auto">
                  <div
                    class="icon icon-shape bg-gradient-info text-white
                    rounded-circle shadow">
                    <i class="ni ni-chart-bar-32" />
                  </div>
                </div>
              </div>
              <p class="mt-3 mb-0 text-sm">
                <span class="text-success mr-2">
                  <i class="fa fa-arrow-up" />
                  3.48%
                </span>
                <span class="text-nowrap">Since last month</span>
              </p>
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
</div>
<!-- Page content -->
<div class="container-fluid mt--6">
  <div class="row">
    <div class="col-xl-8">
      <div class="card">
        <div class="card-header border-0">
          <div class="row align-items-center">
            <div class="col">
              <h3 class="mb-0">Table Mahasiswa</h3>
            </div>
            <div class="col text-right">
              <button
                class="btn btn-sm btn-primary"
                type="button"
                on:click={TambahData}>
                Create
              </button>
            </div>
          </div>
        </div>
        <div class="table-responsive">
          <!-- Projects table -->
          <table class="table align-items-center table-flush">
            <thead class="thead-light">
              <tr>
                <th scope="col">Username</th>
                <th scope="col">Email</th>
                <th scope="col">Password</th>
                <th scope="col">Alamat</th>
                <th scope="col">Tanggal Lahir</th>
                <th scope="col">Hoby</th>
                <th scope="col">Editdata</th>

              </tr>
            </thead>
            <tbody>
              {#each data as list}
                <tr>
                  <td>{list.username}</td>
                  <td>{list.email}</td>
                  <td>{list.password}</td>
                  <td>{list.alamat}</td>

                  <td>
                    <i class="fas fa-arrow-up text-success mr-3" />
                    {list.tgl_lahir}
                  </td>
                  <td>{list.hoby}</td>
                  <td>
                    <a
                      href="/{list._id}"
                      class="btn btn-sm btn-success"
                      rel="prefecth">
                      <i class="ni ni-button-play" />
                      Edit
                    </a>
                  </td>
                </tr>
              {/each}
            </tbody>
          </table>
        </div>
      </div>
    </div>
    <div class="col-xl-4">
      <div class="card">
        <div class="card-header border-0">
          <div class="row align-items-center">
            <div class="col">
              <h3 class="mb-0">Social traffic</h3>
            </div>
            <div class="col text-right">
              <a href="#!" class="btn btn-sm btn-primary">See all</a>
            </div>
          </div>
        </div>
        <div class="table-responsive">
          <!-- Projects table -->
          <table class="table align-items-center table-flush">
            <thead class="thead-light">
              <tr>
                <th scope="col">Referral</th>
                <th scope="col">Visitors</th>
                <th scope="col" />
              </tr>
            </thead>
            <tbody>
              <tr>
                <th scope="row">Facebook</th>
                <td>1,480</td>
                <td>
                  <div class="d-flex align-items-center">
                    <span class="mr-2">60%</span>
                    <div>
                      <div class="progress">
                        <div
                          class="progress-bar bg-gradient-danger"
                          role="progressbar"
                          aria-valuenow="60"
                          aria-valuemin="0"
                          aria-valuemax="100"
                          style="width: 60%;" />
                      </div>
                    </div>
                  </div>
                </td>
              </tr>
              <tr>
                <th scope="row">Facebook</th>
                <td>5,480</td>
                <td>
                  <div class="d-flex align-items-center">
                    <span class="mr-2">70%</span>
                    <div>
                      <div class="progress">
                        <div
                          class="progress-bar bg-gradient-success"
                          role="progressbar"
                          aria-valuenow="70"
                          aria-valuemin="0"
                          aria-valuemax="100"
                          style="width: 70%;" />
                      </div>
                    </div>
                  </div>
                </td>
              </tr>
              <tr>
                <th scope="row">Google</th>
                <td>4,807</td>
                <td>
                  <div class="d-flex align-items-center">
                    <span class="mr-2">80%</span>
                    <div>
                      <div class="progress">
                        <div
                          class="progress-bar bg-gradient-primary"
                          role="progressbar"
                          aria-valuenow="80"
                          aria-valuemin="0"
                          aria-valuemax="100"
                          style="width: 80%;" />
                      </div>
                    </div>
                  </div>
                </td>
              </tr>
              <tr>
                <th scope="row">Instagram</th>
                <td>3,678</td>
                <td>
                  <div class="d-flex align-items-center">
                    <span class="mr-2">75%</span>
                    <div>
                      <div class="progress">
                        <div
                          class="progress-bar bg-gradient-info"
                          role="progressbar"
                          aria-valuenow="75"
                          aria-valuemin="0"
                          aria-valuemax="100"
                          style="width: 75%;" />
                      </div>
                    </div>
                  </div>
                </td>
              </tr>
              <tr>
                <th scope="row">twitter</th>
                <td>2,645</td>
                <td>
                  <div class="d-flex align-items-center">
                    <span class="mr-2">30%</span>
                    <div>
                      <div class="progress">
                        <div
                          class="progress-bar bg-gradient-warning"
                          role="progressbar"
                          aria-valuenow="30"
                          aria-valuemin="0"
                          aria-valuemax="100"
                          style="width: 30%;" />
                      </div>
                    </div>
                  </div>
                </td>
              </tr>
            </tbody>
          </table>
        </div>
      </div>
    </div>
  </div>

  <!-- Footer -->
  <footer class="footer pt-0">
    <div class="row align-items-center justify-content-lg-between">
      <div class="col-lg-6">
        <div class="copyright text-center text-lg-left text-muted">
          &copy; 2020
          <a
            href="https://www.creative-tim.com"
            class="font-weight-bold ml-1"
            target="_blank">
            Creative Tim
          </a>
        </div>
      </div>
      <div class="col-lg-6">
        <ul
          class="nav nav-footer justify-content-center justify-content-lg-end">
          <li class="nav-item">
            <a
              href="https://www.creative-tim.com"
              class="nav-link"
              target="_blank">
              Creative Tim
            </a>
          </li>
          <li class="nav-item">
            <a
              href="https://www.creative-tim.com/presentation"
              class="nav-link"
              target="_blank">
              About Us
            </a>
          </li>
          <li class="nav-item">
            <a
              href="http://blog.creative-tim.com"
              class="nav-link"
              target="_blank">
              Blog
            </a>
          </li>
          <li class="nav-item">
            <a
              href="https://github.com/creativetimofficial/argon-dashboard/blob/master/LICENSE.md"
              class="nav-link"
              target="_blank">
              MIT License
            </a>
          </li>
        </ul>
      </div>
    </div>
  </footer>
</div>
