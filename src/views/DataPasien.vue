<template>
  <div>
    <!-- Navbar -->
    <Navbar />
    <!-- /.navbar -->

    <!-- Main Sidebar Container -->
    <Sidebar />
    <Content />

    <Footer />
  </div>
</template>

<script>
// @ is an alias to /src
import Navbar from "../components/layouts/Navbar.vue";
import Sidebar from "../components/layouts/Sidebar.vue";
import Footer from "../components/layouts/Footer.vue";
import Content from "../components/pasien/Content.vue";
export default {
  name: "DataPasien",
  components: {
    Navbar,
    Sidebar,
    Footer,
    Content,
  },
};
</script>
