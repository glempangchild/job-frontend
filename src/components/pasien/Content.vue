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
              <div class="alert alert-success" role="alert" v-if="success">
                {{ alert.pesan }}
              </div>
              <div class="row">
                <div class="col-lg-12">
                  <div class="text-right">
                    <button
                      @click="modalBacgroundShow = true"
                      type="button"
                      class="btn btn-primary btn-sm"
                      data-toggle="modal"
                      data-target="#addPasienModal"
                    >
                      Add Pasien
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
                          <th>Nama</th>
                          <th>Alamat</th>
                          <th>Jenis Kelamin</th>
                          <th>Tempat Lahir</th>
                          <th>Tanggal Lahir</th>
                          <th>Action</th>
                        </tr>
                      </thead>
                      <tbody>
                        <tr v-for="(person, i) in pasien" :key="i">
                          <td>{{ person.id_pasien }}</td>
                          <td>{{ person.nama }}</td>
                          <td>{{ person.alamat }}</td>
                          <td>{{ person.jenis_kelamin }}</td>
                          <td>{{ person.nama_kota }}</td>
                          <td>{{ person.tanggal_lahir }}</td>
                          <td>
                            <button
                              @click="getEditData(person)"
                              type="button"
                              class="btn btn-primary btn-sm"
                            >
                              Edit</button
                            >&nbsp;
                            <button @click="deleteData(person.id_pasien)" type="button" class="btn btn-sm btn-danger">
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
    <!-- END MAIN -->
    <!-- Modal -->
    <div
      class="modal fade"
      id="addPasienModal"
      tabindex="-1"
      role="dialog"
      aria-labelledby="exampleModalLabel"
      aria-hidden="true"
      v-if="modalBacgroundShow"
    >
      <div class="modal-dialog" role="document">
        <div class="modal-content">
          <div class="modal-header">
            <h5 class="modal-title" id="exampleModalLabel">Add Data Pasien</h5>
            <button
              type="button"
              class="close"
              data-dismiss="modal"
              aria-label="Close"
            >
              <span aria-hidden="true">&times;</span>
            </button>
          </div>
          <div class="modal-body">
            <div class="row">
              <div class="form-group col-md-6">
                <label for="i">Nama</label>
                <input
                  v-model="data.nama"
                  type="text"
                  class="form-control"
                  id="nama"
                  placeholder="Nama Lengkap"
                />
              </div>
              <div class="form-group col-md-6">
                <label for="">Alamat</label>
                <textarea
                  v-model="data.alamat"
                  class="form-control"
                  id="alamat"
                  rows="3"
                ></textarea>
              </div>
            </div>
            <div class="row">
              <div class="form-group col-md-4">
                <label for="inputEmail4">Jenis Kelamin</label>
                <select
                  v-model="data.jenis_kelamin"
                  id="jenisKelamin"
                  class="form-control"
                >
                  <option selected>Choose...</option>
                  <option value="L">Laki-Laki</option>
                  <option value="P">Perempuan</option>
                </select>
              </div>
              <div class="form-group col-md-4">
                <label for="inputEmail4">Provinsi</label>
                <select
                  v-model="provinsiV"
                  @change="onChange($event)"
                  id="provinsi"
                  class="form-control"
                >
                  <option selected>Pilih Provinsi</option>
                  <option
                    v-for="(prov, i) in provinsi"
                    :key="i"
                    :value="prov.id_provisni"
                    >{{ prov.nama_provinsi }}</option
                  >
                </select>
              </div>
              <div class="form-group col-md-4">
                <label for="inputEmail4">Tempat Lahir</label>
                <select v-model="data.id_kota" id="kota" class="form-control">
                  <option selected>Pilih Kota</option>
                  <option
                    v-for="(item, i) in kota"
                    :key="i"
                    :value="item.id_kota"
                    >{{ item.nama_kota }}</option
                  >
                </select>
              </div>
            </div>
            <div class="row">
              <div class="form-group col-md-6">
                <label for="inputEmail4">Tanggal Lahir</label>
                <input
                  v-model="data.tanggal_lahir"
                  class="form-control"
                  type="date"
                  id="tanggalLahir"
                />
              </div>
              <div class="form-group col-md-6"></div>
            </div>
            <div class="row">
              <div class="form-group col-md-12">
                <button v-on:click="tambahPasien()" class="btn btn-primary">
                  Simpan
                </button>
              </div>
            </div>
          </div>
          <div class="modal-footer"></div>
        </div>
      </div>
    </div>
    <!-- Edit Modal -->
    <editModal
      v-on:test="changeAlert($event)"
      :dataPasien="editData"
      :dataProvinsi="provinsi"
      :dataKota="kota"
      v-if="editModal"
      @close="editModal=false"
    ></editModal>
    <!-- End Edit Modal -->
  </div>
</template>
<script>
import editModal from "./EditModal.vue";
import axios from "axios";
import jQuery from "jquery";
const $ = jQuery;
window.$ = $;
export default {
  data() {
    return {
      // modalShow: false,
      modalBacgroundShow: true,
      editModal: false,
      editData: null,
      alert: {
        pesan: "",
        error: "",
      },
      kota: [],
      provinsiV: "",
      provinsi: [],
      pasien: [],
      data: {
        nama: "",
        alamat: "",
        jenis_kelamin: "",
        id_kota: null,
        tanggal_lahir: "",
      },
      success: false,
    };
  },
  methods: {
    showAlert(v) {
      this.success = v;
    },
    async getProvinsi() {
      await axios
        .get(`http://localhost/phprest/api/pasien/readProvinsi.php`)
        .then((response) => {
          // JSON responses are automatically parsed.
          if (response.data.message == "No Posts Found") {
            this.provinsi = [];
          } else {
            this.provinsi = response.data;
          }
        })
        .catch((e) => {
          this.errors.push(e);
        });
    },
    getKota() {
      var self = this;
      $.ajax({
        url: "http://localhost/phprest/api/pasien/readKota.php",
        type: "POST",
        dataType: "json",
        data: JSON.stringify({ id_provinsi: self.provinsiV }),
        success: function(response) {
          if (response["message"] === "NoData") {
            self.kota = [];
          } else {
            self.kota = response;
          }
        },
      });
    },
    onChange() {
      this.getKota();
    },
    changeAlert(msg){
      this.success = msg.alert;
      this.alert.pesan = msg.message;
    },
    getEditData(person) {
      this.editData = person;
      this.editModal = true;
    },
    deleteData(id){
      let self = this;
      $.ajax({
        url: "http://localhost/phprest/api/pasien/delete.php",
        type: "DELETE",
        dataType: "json",
        data: JSON.stringify({ id_pasien: id }),
        success: function(response) {
          if (response["message"] === "Post Deleted") {
            self.tampilPasien();
          } else {
            console.log('wrong');
          }
        },
      });
    },
    tambahPasien() {
      var self = this;
      $.ajax({
        url: "http://localhost/phprest/api/pasien/create.php",
        type: "POST",
        dataType: "json",
        data: JSON.stringify(this.data),
        success: function(data) {
          if (data["message"] === "Post Created") {
            self.success = true;
          } else {
            console.log("ngga");
          }
        },
      });
    },
    async tampilPasien() {
      await axios
        .get(`http://localhost/phprest/api/pasien/read.php`)
        .then((response) => {
          // JSON responses are automatically parsed.
          if (response.data.message == "No Posts Found") {
            this.pasien = [];
          } else {
            this.pasien = response.data;
          }
        })
        .catch((e) => {
          this.errors.push(e);
        });
    },
  },
  components: {
    editModal,
  },
  mounted() {
    this.tampilPasien();
    this.getProvinsi();
    this.getKota();
  },
};
</script>
