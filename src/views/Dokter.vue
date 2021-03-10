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
import Navbar from "../components/layouts/Navbar.vue";
import Sidebar from "../components/layouts/Sidebar.vue";
import Footer from "../components/layouts/Footer.vue";
import Content from "../components/dokter/Content.vue";
export default {
  name: "Dokter",
  components: {
    Navbar,
    Sidebar,
    Footer,
    Content,
  },
};
</script>
