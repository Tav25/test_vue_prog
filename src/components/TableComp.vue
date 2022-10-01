<template>
  <div class="hello">
    <h3>TableComp</h3>
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
          <tr v-for="(dataCell, index) in dataTab" :key="dataCell.id" >
            <td>{{dataCell.id}}</td>
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
            <li class="page-item"  v-for="(pagNum, index) in lengthDataTab" :class="{ 'fw-bold' : currentPage === index + 1 }" :key="pagNum">
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
  </div>
  <ul>
    <li v-for="g in info" :key="g">>>{{ g }}</li>
  </ul>
  {{ lengthDataTab }} ct {{countTab}}
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
      dataTab: {},
      currentPage: 1,
      countRow: 50,
      rowNumber: 1,
      countTab: 0
    }
  },

  computed: {
    lengthDataTab () {
      return Object.keys(this.dataTab).length / this.countRow
    }

    // rowNumberUpdate () {
    //   return this.rowNumber + 1
    // }
  },

  filters: {
    capitalize: function (value) {
      if (!value) return ''
      value = value.toString()
      return value.charAt(0).toUpperCase() + value.slice(1)
    }
  },

  mounted () {
    const self = this
    axios
      .get('http://192.168.100.62:3000/api/data50')
      .then(function (response) {
        self.dataTab = response.data
      })

    axios
      .get('http://192.168.100.62:3000/api/count')
      .then(function (response) {
        self.countTab = response.data[0]['count(*)']
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
