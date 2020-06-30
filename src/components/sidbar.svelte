<script>
  export let segment;
</script>

<!-- Sidenav -->
<nav
  class="sidenav navbar navbar-vertical fixed-left navbar-expand-xs navbar-light
  bg-white"
  id="sidenav-main">
  <div class="">
    <!-- Brand -->
    <div class="sidenav-header align-items-center">
      <a class="navbar-brand" href=".">
        <img
          src="../assets/img/brand/blue.png"
          class="navbar-brand-img"
          alt="..." />
      </a>
    </div>
    <div class="navbar-inner">
      <!-- Collapse -->
      <div class="collapse navbar-collapse" id="sidenav-collapse-main">
        <!-- Nav items -->
        <ul class="navbar-nav">
          <li class="nav-item">
            <a
              class={segment === undefined ? 'nav-link active' : 'nav-link '}
              href=".">
              <i class="ni ni-tv-2 text-primary" />
              <span class="nav-link-text">Dashboard</span>
            </a>
          </li>
          <li class="nav-item">
            <a class="nav-link" href="examples/icons.html">
              <i class="ni ni-planet text-orange" />
              <span class="nav-link-text">Icons</span>
            </a>
          </li>

        </ul>
        <!-- Divider -->
        <!-- Navigation -->

      </div>
    </div>
  </div>
</nav>
