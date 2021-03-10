<template>
  <div id="sidebar-nav" class="sidebar">
    <div class="sidebar-scroll">
      <nav>
        <ul class="nav">
          <li>
            <a href="index.html" class="active"
              ><i class="fas fa-hospital"></i><span>Dashboard</span></a
            >
          </li>
          <li>
            <a href="#subPages" data-toggle="collapse" class="collapsed"
              ><i class="fas fa-head-side-cough"></i><span>Pasien</span>
              <i class="icon-submenu lnr lnr-chevron-left"></i
            ></a>
            <div id="subPages" class="collapse ">
              <ul class="nav">
                <li>
                  <router-link :to="{ name: 'DataPasien' }" class="nav-link">
                    <p>Data Pasien</p>
                  </router-link>
                </li>
                <li>
                  <a href="page-login.html" class="">Pendaftaran Pasien</a>
                </li>
              </ul>
            </div>
          </li>
          <li>
            <a href="#subDokter" data-toggle="collapse" class="collapsed"
              ><i class="fas fa-user-md"></i> <span>Dokter</span>
              <i class="icon-submenu lnr lnr-chevron-left"></i
            ></a>
            <div id="subDokter" class="collapse ">
              <ul class="nav">
                <li><a href="page-profile.html" class="">Data Dokter</a></li>
                <li>
                  <a href="page-login.html" class="">Specialist</a>
                </li>
              </ul>
            </div>
          </li>
          <li>
            <a href="charts.html" class=""
              ><i class="fas fa-viruses"></i> <span>Penyakit</span></a
            >
          </li>
          <li>
            <a href="panels.html" class=""
              ><i class="fas fa-procedures"></i> <span>Poli</span></a
            >
          </li>
          <li>
            <a href="#subFarmasi" data-toggle="collapse" class="collapsed"
              ><i class="fas fa-pills"></i> <span>Farmasi</span>
              <i class="icon-submenu lnr lnr-chevron-left"></i
            ></a>
            <div id="subFarmasi" class="collapse ">
              <ul class="nav">
                <li><a href="page-profile.html" class="">Data Obat</a></li>
                <li>
                  <a href="page-login.html" class="">Stok Obat</a>
                </li>
                <li>
                  <a href="page-login.html" class="">Pemaikaian</a>
                </li>
              </ul>
            </div>
          </li>
          <li>
            <a href="tables.html" class=""
              ><i class="fas fa-file"></i><span>Administrasi</span></a
            >
          </li>
        </ul>
      </nav>
    </div>
  </div>
</template>
<script>
export default {};
</script>
