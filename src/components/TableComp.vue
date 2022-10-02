<template>
  <div class="container" v-cloak>
    <h3>TableComp</h3>
    <div class="col-xl-8 col-xxl-8 mx-auto" >
      <div class="row filters">
        <div class="col">
          <select v-model="paramsAxios.sort">
            <optgroup label="select column">
              <option value="name">Name</option>
              <option value="quantity">Current</option>
              <option value="distance">Distance</option>
            </optgroup>
          </select>
          <select v-model="paramsAxios.type">
            <optgroup label="select filter param">
              <option value="equals">=</option>
              <option value="less">&lt;</option>
              <option value="more">&gt;</option>
            </optgroup>
          </select>
          <input
            type="text"
            v-model="paramsAxios.data"
            @keypress.enter="
              paramsAxios.currentPage = 1;
              main();
            "
          />
          <button
            class="btn btn-primary btn-sm"
            @click="
              paramsAxios.currentPage = 1;
              main();
            "
          >
            filter
          </button>
          <button
            class="btn btn-danger btn-sm"
            @click="
              paramsAxios.currentPage = 1;
              paramsAxios.sort = '';
              paramsAxios.data = '';
              paramsAxios.type = '';
              main();
            "
          >
            reset
          </button>
        </div>
      </div>
      <div class="row" v-if="dataTab.length>0" >
      <div class="table-responsive">
        <table class="table table-striped table-sm table-bordered">
          <thead class="text-center">
            <tr>
              <!-- <th>#</th> -->
              <th>Date</th>
              <th>Name</th>
              <th>Curent</th>
              <th>Distance</th>
            </tr>
          </thead>
          <tbody>
            <tr v-for="dataCell in dataTab" :key="dataCell.id">
              <!-- <td>{{ dataCell.id }}</td> -->
              <td>{{ dataCell.date }}</td>
              <td>{{ dataCell.name }}</td>
              <td>{{ dataCell.quantity }}</td>
              <td>{{ dataCell.distance }}</td>
            </tr>
          </tbody>
        </table>
      </div>
      <div class="row">
        <div class="col">
          <nav class="d-xl-flex justify-content-xl-center">
            <ul class="pagination pagination-sm">
              <li class="page-item">
                <a
                  class="page-link"
                  aria-label="Previous"
                  href="#"
                  @click="
                    if (paramsAxios.currentPage > 1) {
                      paramsAxios.currentPage--;
                      main();
                    }
                  "
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
                  main();
                "
              >
                <a class="page-link" href="#">{{ pagNum }}</a>
              </li>
              <li class="page-item">
                <a
                  class="page-link"
                  aria-label="Next"
                  href="#"
                  @click="
                    if (paramsAxios.currentPage < lengthDataTab) {
                      paramsAxios.currentPage++;
                      main();
                    }
                  "
                  ><span aria-hidden="true">»</span></a
                >
              </li>
            </ul>
          </nav>
        </div>
      </div>
      <div class="row">
        <div class="col">
          <nav class="d-xl-flex justify-content-xl-center">
            <ul class="pagination pagination-sm">
              <li
                class="page-item"
                @click="
                  paramsAxios.limitRow = 10;
                  paramsAxios.currentPage = 1;
                  this.main();
                "
                :class="{ 'fw-bold': paramsAxios.limitRow === 10 }"
              >
                <a class="page-link" href="#"
                  ><span aria-hidden="true">10</span></a
                >
              </li>
              <li
                class="page-item"
                @click="
                  paramsAxios.limitRow = 25;
                  paramsAxios.currentPage = 1;
                  this.main();
                "
                :class="{ 'fw-bold': paramsAxios.limitRow === 25 }"
              >
                <a class="page-link" href="#"
                  ><span aria-hidden="true">25</span></a
                >
              </li>
              <li
                class="page-item"
                @click="
                  paramsAxios.limitRow = 50;
                  paramsAxios.currentPage = 1;
                  this.main();
                "
                :class="{ 'fw-bold': paramsAxios.limitRow === 50 }"
              >
                <a class="page-link" href="#"
                  ><span aria-hidden="true">50</span></a
                >
              </li>
            </ul>
          </nav>
        </div>
      </div>
    </div>
    <div v-else>no data</div>
    </div>
  </div>
</template>

<script>
const axios = require('axios').default
export default {
  name: 'TableComp',

  data () {
    return {
      // url: 'http://localhost:3000',
      url: 'https://sheltered-eyrie-29185.herokuapp.com',
      dataTab: [''],
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
    main () {
      const self = this
      axios
        .get(`${this.url}/data`, {
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
    this.main()
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped lang="scss">
input,
select,
button {
  height: 30px;
  margin-right: 10px;
}

.filters {
  margin-bottom: 20px;
}

[v-cloak] {
  display: none;
}
</style>
