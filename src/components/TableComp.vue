<template>
  <div class="hello">
    <h3>TableComp</h3>

    <div>
      <select v-model="paramsAxios.sort">
        <optgroup label="select column" >
          <option value="12" selected>-</option>
          <option value="name">Name</option>
          <option value="quantity">Current</option>
          <option value="distance">Distance</option>
        </optgroup>
      </select>
      <select v-model="paramsAxios.type" >
        <optgroup label="select filter param">
          <option value="equals">=</option>
          <option value="less">&lt;</option>
          <option value="more">&gt;</option>
        </optgroup>
      </select>
      <input type="text" v-model="paramsAxios.data" />
      <button
      class="btn btn-primary btn-sm"
      @click="
        paramsAxios.currentPage = 1;
        gh();
      "
    >
      filter</button
    >
    </div>
    <div class="table-responsive">
      <table class="table table-striped table-sm table-bordered">
        <thead class="text-center">
          <tr>
            <th>#</th>
            <th>Date</th>
            <th>Name</th>
            <th>Curent</th>
            <th>Distance</th>
          </tr>
        </thead>
        <tbody>
          <tr v-for="(dataCell, index) in dataTab" :key="dataCell.id">
            <td>{{ dataCell.id }}</td>
            <td>{{ dataCell.date }}_{{ index }}</td>
            <td>{{ dataCell.name }}</td>
            <td>{{ dataCell.quantity }}</td>
            <td>{{ dataCell.distance }}</td>
          </tr>
        </tbody>
      </table>
    </div>
    <div class="row">

      <div class="col-md-4">
        <nav>
          <ul class="pagination pagination-sm">
            <li class="page-item">
              <a class="page-link" aria-label="Previous" href="#"
                ><span aria-hidden="true">«</span></a
              >
            </li>
            <li
              class="page-item"
              v-for="(pagNum, index) in lengthDataTab"
              :class="{ 'fw-bold': paramsAxios.currentPage === index + 1 }"
              :key="pagNum"
              @click="paramsAxios.currentPage = index + 1 ; gh()">
              <a class="page-link" href="#">{{ pagNum }}</a>
            </li>
            <li class="page-item">
              <a class="page-link" aria-label="Next" href="#"
                ><span aria-hidden="true">»</span></a
              >
            </li>
          </ul>
        </nav>
      </div>

    </div>
    <button
      class="btn btn-danger"
      @click="
        paramsAxios.limitRow = 10;
        paramsAxios.currentPage = 1;
        this.gh();
      "
    >
      10
    </button>
    <button
      class="btn btn-danger"
      @click="
        paramsAxios.limitRow = 25;
        paramsAxios.currentPage = 1;
        this.gh();
      "
    >
      25
    </button>
    <button
      class="btn btn-danger"
      @click="
        paramsAxios.limitRow = 50;
        paramsAxios.currentPage = 1;
        this.gh();
      "
    >
      50
    </button>
  </div>
</template>

<script>
const axios = require('axios').default
export default {
  name: 'TableComp',

  data () {
    return {
      test: 1,
      dataTab: {},
      totalPaginationPages: '',
      paramsAxios: {
        sort: '',
        data: '',
        type: '=',
        limitRow: 25,
        currentPage: 1
      }
    }
  },

  methods: {
    gh () {
      const self = this
      axios
        .get('http://localhost:3000/api/d', {
          params: self.paramsAxios
        })
        .then(function (response) {
          self.dataTab = response.data.result
          self.totalPaginationPages = response.data.count
        })
    }
  },

  computed: {
    lengthDataTab () {
      return Math.ceil(this.totalPaginationPages / this.paramsAxios.limitRow)
    }
  },

  mounted () {
    this.gh()
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped lang="scss">
input {
  height: 22px;
}
</style>
