<template>
  <div class="detail">

    <div class="container text-left">
      <div class="card mb-3">
        <div class="card-header bg-primary text-white">
          <h5 class="card-title m-0">
            Data Register Barang Bukti
          </h5>
        </div>
        <div class="card-body">
          <tr>
            <td width="170px">Nomer Register</td>
            <td>: {{ evidence.register_number }}</td>
          </tr>
          <tr>
            <td>Tanggal Register</td>
            <td>: {{ evidence.register_date }}</td>
          </tr>
          <tr>
            <td>Nama Tersangka</td>
            <td>: {{ evidence.suspect }}</td>
          </tr>
          <tr>
            <td>Pasal Kejahatan</td>
            <td>: {{ evidence.article }}</td>
          </tr>
          <tr>
            <td>Nama Jaksa</td>
            <td>: {{ evidence.prosecutor }}</td>
          </tr>
        </div>
      </div>


    </div>

    <div class="container text-left" v-if="detailEvidence.length > 0">
      <div class="card mb-3" v-for="detail in detailEvidence" v-bind:key="detail.id">
        <div class="card-header">
          <h5 class="card-title m-0">
            Detail Barang Bukti
          </h5>
        </div>
        <div class="card-body">

          <tr>
            <td width="170px">Nama Barang Bukti</td>
            <td>: {{ detail.name }}</td>
          </tr>
          <tr>
            <td>Kriteria</td>
            <td>: {{ detail.criteria.name }}</td>
          </tr>
          <tr>
            <td>Jumlah</td>
            <td>: {{ detail.amount }}</td>
          </tr>
          <tr>
            <td>Keterangan Detail</td>
            <td>: {{ detail.description }}</td>
          </tr>
          <tr>
            <td>Gambar Barang Bukti</td>
            <td>

              <div class="" v-if="detail.images.length > 0">
                :
                <ul v-for="image in detail.images" v-bind:key="image.id">
                  <li>
                    <div class="card w-50">
                      <img v-bind:src="image.image" alt="" class="card-img-top">
                    </div>
                  </li>
                </ul>
              </div>
              <div class="" v-else>: Gambar Tidak Tersedia</div>

            </td>
          </tr>

        </div>
      </div>
    </div>

    <div class="" v-else>
      Detail Barang Bukti Tidak Tersedia
    </div>
  </div>
</template>

<script>

import axios from 'axios'

export default {
  name: 'Detail',
  components: {

  },
  data() {
    return {
      evidence: [],
      detailEvidence: []
    }
  },
  mounted () {
    axios
      .get('http://127.0.0.1:8000/api/evidence/', {
        params: {
          id: this.$route.params.id
        }
      })
      .then(response => (this.evidence = response.data.data)),  
    axios
      .get('http://127.0.0.1:8000/api/evidence/detail', {
        params: {
          id: this.$route.params.id
        }
      })
      .then(response => (this.detailEvidence = response.data.data))  
  }  

}
</script>