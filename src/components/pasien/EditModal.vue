<template>
  <div class="modal" id="myModal" style="display: block;">
    <div class="modal-dialog" role="document">
      <div class="modal-content">
        <!-- Modal Header -->
        <div class="modal-header">
          <h4 class="modal-title">Edit Data Pasien</h4>
          <button
            type="button"
            class="close"
            @click="$emit('close')"
            data-dismiss="modal"
          >
            ×
          </button>
        </div>
        <!-- Modal body -->
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
                  v-for="(prov, i) in dataProvinsi"
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
        </div>
        <!-- Modal footer -->
        <div class="modal-footer">
          <button
            v-on:click="editPasien()"
            class="btn btn-primary"
          >
            Simpan
          </button>
          <button  v-on:click="changeValue()">EMIT</button>
        </div>
      </div>
    </div>
  </div>
</template>
<script>
import axios from "axios";
import jQuery from "jquery";
const $ = jQuery;
window.$ = $;
export default {
  data() {
    return {
      nilaiEmit:{
        message:"Testing Emit",
        alert:false
      },
      kota: [],
      provinsiV: null,
      data: {
        id_pasien: this.dataPasien.id_pasien,
        nama: this.dataPasien.nama,
        alamat: this.dataPasien.alamat,
        jenis_kelamin: "",
        id_kota: null,
        tanggal_lahir: "",
      },
    };
  },
  methods: {
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
    changeValue: function(){
      this.$emit('test', this.nilaiEmit);
      console.log('must show');
    },
    async editPasien() {
      //   let self = this;
      //   await $.ajax({
      //   url: "http://localhost/phprest/api/pasien/update.php",
      //   type: "PUT",
      //   dataType: "json",
      //   data: JSON.stringify(this.data),
      //   success: function(data) {
      //     if (data["message"] === "Post Updated") {
      //         console.log('edited');
      //         self.$emit('test', self.nilaiEmit);
      //     } else {
      //       console.log("ngga");
      //     }
      //   },
      // });
        axios.post('http://localhost/phprest/api/pasien/update.php', JSON.stringify(this.data))
        .then(response => {
          this.nilaiEmit.alert = true;
          this.nilaiEmit.message = response.data['message'];
          this.$emit('test', this.nilaiEmit);
          this.$emit('close');
        })
        .catch(error => {
          console.log('NO ' , error);
        });
    },
  },
  props: ["dataPasien", "dataProvinsi", "dataKota"],
};
</script>
