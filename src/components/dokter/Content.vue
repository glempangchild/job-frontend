<template>
    <div>
    <!-- MAIN -->
    <div class="main">
      <!-- MAIN CONTENT -->
      <div class="main-content">
        <div class="container-fluid">
          <!-- OVERVIEW -->
          <div class="panel panel-headline">
            <div class="panel-heading">
              <h3 class="panel-title">Weekly Overview</h3>
              <p class="panel-subtitle">Period: Oct 14, 2016 - Oct 21, 2016</p>
            </div>
            <div class="panel-body">
              <div class="alert alert-success" role="alert" >
              </div>
              <div class="row">
                <div class="col-lg-12">
                  <div class="text-right">
                    <button
                        @click="tampilInsertModal()"
                        type="button"
                        class="btn btn-primary btn-sm"
                    >
                      Tambah Dokter
                    </button>
                  </div>
                </div>
              </div>
              <br />
              <div class="row">
                <div class="col-lg-12">
                  <div class="table-responsive">
                    <table class="table table-hover">
                      <thead>
                        <tr>
                          <th>Id</th>
                          <th>Nama Dokter</th>
                          <th>Jenis Kelamin</th>
                          <th>Telphone</th>
                          <th>Alamat</th>
                          <th>Keahlian</th>
                          <th>Action</th>
                        </tr>
                      </thead>
                      <tbody>
                        <tr>
                          <td></td>
                          <td></td>
                          <td></td>
                          <td></td>
                          <td></td>
                          <td></td>
                          <td>
                            <button
                              type="button"
                              class="btn btn-primary btn-sm"
                            >
                              Edit</button
                            >&nbsp;
                            <button type="button" class="btn btn-sm btn-danger">
                              Hapus
                            </button>
                          </td>
                        </tr>
                      </tbody>
                    </table>
                  </div>
                </div>
              </div>
            </div>
          </div>
          <!-- END OVERVIEW -->
        </div>
      </div>
      <!-- END MAIN CONTENT -->
    </div>
    <insertModal
      v-if="showInsertModal"
      @close="showInsertModal=false"
    ></insertModal>
  </div>
</template>
<script>
import insertModal from "./InsertModal.vue";
export default {
    data(){
        return{
            showInsertModal: false,
        }
    },
    components: {
    insertModal,
  },
  methods: {
      tampilInsertModal() {
      this.showInsertModal = true;
    },
  },
}
</script>