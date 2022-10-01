<template>
  <div class="hello">
    <h3>TableComp</h3>

    <button
      class="btn btn-danger"
      @click="
        test = test + 1;
        gh();
      "
    >
      Update</button
    >{{ test }}
    <div>
      <select>
        <optgroup label="select column">
          <option value="12" selected>-</option>
          <option value="12">Name</option>
          <option value="13">Current</option>
          <option value="14">Distance</option>
        </optgroup>
      </select>
      <select>
        <optgroup label="select filter param">
          <option value="12" selected>=</option>
          <option value="13">&lt;</option>
          <option value="14">&gt;</option>
        </optgroup>
      </select>
      <input type="text" />
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
      <div class="col-md-4"></div>
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
              @click="
                paramsAxios.currentPage = index + 1;
                gh();
              "
            >
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
      <div class="col-md-4"></div>
    </div>
    <button
      class="btn btn-danger"
      @click="
        paramsAxios.limitRow = 10;
        paramsAxios.currentPage = 1;
        gh();
      "
    >
      10
    </button>
    <button
      class="btn btn-danger"
      @click="
        paramsAxios.limitRow = 25;
        paramsAxios.currentPage = 1;
        gh();
      "
    >
      25
    </button>
    <button
      class="btn btn-danger"
      @click="
        paramsAxios.limitRow = 50;
        paramsAxios.currentPage = 1;
        gh();
      "
    >
      50
    </button>
  </div>
  <!-- <ul>
    <li v-for="g in info" :key="g">>>{{ g }}</li>
  </ul> -->
  <!-- {{dataTab}}d -->
</template>

<script>
const axios = require('axios').default
export default {
  name: 'TableComp',
  props: {
    msg: String
  },

  data () {
    return {
      test: 1,
      dataTab: {},
      countRow: 50,
      totalPaginationPages: '',
      paramsAxios: {
        sort: '',
        data: '',
        type: '',
        limitRow: 25,
        currentPage: 1
      }
    }
  },

  methods: {
    gh () {
      console.log('>>>>')
      console.log(this.paramsAxios)
      // this.paramsAxios.currentPage = 1
      // this.paramsAxios.sort = 'id'
      // this.paramsAxios.data = '55'
      // this.paramsAxios.type = 'less'

      // console.log(this.paramsAxios)
      ///
      const self = this
      axios
        .get('http://192.168.100.62:3000/api/d', {
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
      // return this.totalPaginationPages / this.paramsAxios.limitRow
    }
  },

  mounted () {
    const self = this
    axios
      .get('http://192.168.100.62:3000/api/d', {
        params: self.paramsAxios
      })
      .then(function (response) {
        self.dataTab = response.data.result
        self.totalPaginationPages = response.data.count
      })
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped lang="scss">
input {
  height: 22px;
}
</style>
