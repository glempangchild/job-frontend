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
            <input type="text" class="form-control" id="namaDokter" placeholder="Nama Dokter">
          </div>
          <div class="form-group">
            <label for="">Jenis Kelamin</label>
            <select class="form-control" id="kelamin">
              <option>L</option>
              <option>P</option>
            </select>
          </div>
          <div class="form-group">
            <label for="">No Telphone</label>
            <input type="text" class="form-control" id="noTelphone" placeholder="Nama Dokter">
          </div>
          <div class="form-group">
            <label for="exampleFormControlTextarea1">Alamat Lengkap</label>
            <textarea class="form-control" id="alamat" rows="3"></textarea>
          </div>
          <div class="form-group">
            <label for="">Keahlian</label>
            <select class="form-control" id="kelamin">
              <option>Umum</option>
              <option>Kulit</option>
            </select>
          </div>
        </div>
        <!-- Modal footer -->
        <div class="modal-footer">
          <button
            @click="$emit('close')"
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
export default {
    
}
</script>