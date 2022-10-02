<template>
  <header
    class="d-xl-flex justify-content-xl-center"
    style="background: var(--bs-link-hover-color); margin-bottom: 50px"
  >
    <a
      href="https://tav25.github.io/cv/"
      target="_blank"
      style="color: var(--bs-gray-400)"
      >Турбин Александр</a
    >
  </header>
  <TableComp></TableComp>
</template>

<script>
import TableComp from './components/TableComp.vue'

export default {
  name: 'App',
  components: {
    TableComp
  }
}
</script>

<style lang="scss">
@import "bootstrap/scss/bootstrap";
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  // margin-top: 60px;
}
</style>
