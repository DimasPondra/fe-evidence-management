<template>
  <div class="home">

    <div class="container table-responsive">

      <h1 class="pb-4">Data Barang Bukti Kejaksaan</h1>

      <table class="table table-bordered">
        <thead class="thead-dark">
          <tr>
            <th scope="col">Nomer Register</th>
            <th scope="col">Tanggal Register</th>
            <th scope="col">Nama Tersangka</th>
            <th scope="col">Pasal Kejahatan</th>
            <th scope="col">Nama Jaksa</th>
            <th scope="col">Action</th>
          </tr>
        </thead>
        <tbody v-if="evidence.length > 0">

          <tr v-for="itemEvidence in evidence" v-bind:key="itemEvidence.id">
            <th scope="row">{{ itemEvidence.register_number }}</th>
            <td>{{ itemEvidence.register_date }}</td>
            <td>{{ itemEvidence.suspect }}</td>
            <td>{{ itemEvidence.article }}</td>
            <td>{{ itemEvidence.prosecutor }}</td>
            <td>
              <router-link class="btn btn-primary" v-bind:to="'/detail/' + itemEvidence.id ">
                Lihat Detail
              </router-link>
            </td>
          </tr>

        </tbody>

        <tbody v-else>
          <tr>
            <td colspan="6">
              Data Tidak Tersedia
            </td>
          </tr>
        </tbody>
      </table>
      
    </div>

  </div>
</template>

<script>

import axios from 'axios'

export default {
  name: 'Home',
  components: {
    
  },
  data () {
    return {
      evidence: []
    }
  },
  mounted () {
    axios
      .get('http://127.0.0.1:8000/api/evidence')
      .then(response => (this.evidence = response.data.data))
  }
}
</script>
