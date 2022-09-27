<template>
  <div class="hello">
    <h3>TableComp</h3>
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
          <tr>
            <td>Cell 1</td>
            <td>Cell 2</td>
            <td>Cell 2</td>
            <td>Cell 3</td>
            <td>Cell 3</td>
          </tr>
          <tr>
            <td>Cell 3</td>
            <td>Cell 2</td>
            <td>Cell 4</td>
            <td>Cell 3</td>
            <td>Cell 3</td>
          </tr>
        </tbody>
      </table>
    </div>
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
  </div>
</template>

<script>
export default {
  name: 'TableComp',
  props: {
    msg: String
  },

  data () {
    return {
      x: 10
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped lang="scss">
input{
  height: 22px;
}
</style>
