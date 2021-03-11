<template>
   <div class="modal" id="myModal" style="display: flex;">
    <div class="modal-dialog" role="document">
      <div class="modal-content">
        <!-- Modal Header -->
        <div class="modal-header">
          <h4 class="modal-title">Tambah Data Pasien</h4>
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
          <div class="form-group">
            <label for="">Nama Dokter</label>
            <input
            v-model="data.nama_dokter" 
            type="text" class="form-control" id="namaDokter" placeholder="Nama Dokter">
          </div>
          <div class="form-group">
            <label for="">Jenis Kelamin</label>
            <select
            v-model="data.jenis_kelamin"
            class="form-control" id="kelamin">
              <option>L</option>
              <option>P</option>
            </select>
          </div>
          <div class="form-group">
            <label for="">No Telphone</label>
            <input
            v-model="data.telphone" 
            type="text" class="form-control" id="noTelphone" placeholder="Nama Dokter">
          </div>
          <div class="form-group">
            <label for="exampleFormControlTextarea1">Alamat Lengkap</label>
            <textarea
            v-model="data.alamat" 
            class="form-control" id="alamat" rows="3"></textarea>
          </div>
          <div class="form-group">
            <label for="">Keahlian</label>
            <select
            @change="onChange($event)" 
            class="form-control" id="spesialis"
            >
              <option>Pilih Keahlian</option>
              <option
                    v-for="(sep, i) in spesialis"
                    :key="i"
                    :value="sep.id_spesialis"
                    >{{ sep.spesialis }}</option
                  >
            </select>
          </div>
        </div>
        <!-- Modal footer -->
        <div class="modal-footer">
          <button
            v-on:click="tambahDokter()"
            class="btn btn-primary"
          >
            Simpan
          </button>
        </div>
      </div>
    </div>
  </div>
</template>
<script>
import axios from "axios";
export default {
    data(){
      return{
        data: {
        nama_dokter: "",
        jenis_kelamin: "",
        telphone: "",
        alamat: "",
        id_spesialis: null,
      },
        dokterV:'',
        spesialis: [],
        alert: {
          pesan: '',
          error: ''
        }
      }
    },
    methods: {
        getSpesialis(){
        axios.get('http://localhost/phprest/api/spesialis/read.php')
          .then(response => {
            this.spesialis = response.data.data;
          })
          .catch(error => {
            console.log('NO' , error);
          });
      },
      onChange(event) {
        this.data.id_spesialis = event.target.value;
      },
      tambahDokter(){
        axios.post('http://localhost/phprest/api/dokter/create.php', JSON.stringify(this.data))
        .then(response => {
          this.alert.pesan = response.data['message'];
          this.alert.error = true;
          this.$emit('test', this.alert);
          this.$emit('close');
        })
        .catch(error => {
          console.log('NO ' , error);
        });
      }
    },
    created() {
      this.getSpesialis();
    },
}
</script>