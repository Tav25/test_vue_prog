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
          <tr v-for="dataCell in dataTab" :key="dataCell.id">
            <td>{{dataCell.id}}</td>
            <td>{{dataCell.date}}</td>
            <td>{{dataCell.name}}</td>
            <td>{{dataCell.quantity}}</td>
            <td>{{dataCell.distance}}</td>
          </tr>
        </tbody>
      </table>
    </div>

  </div>
  <ul>
      <li v-for="g in info" :key="g">>>{{ g }}</li>
    </ul>
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
      dataTab: {}
    }
  },
  mounted () {
    const self = this
    axios
      .get('http://192.168.100.62:3000/api/data/')
      .then(function (response) {
        // handle success
        self.dataTab = response.data
        console.log(response)
      })
      .catch(function (error) {
        // handle error
        console.log(error)
      })
      .finally(function () {
        // always executed
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
