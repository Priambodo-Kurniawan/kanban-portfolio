<template>
  <div id="app">
    <!-- <img src="./assets/logo.png"> -->
    <router-view></router-view>
  </div>
</template>

<script>
export default {
  name: 'app'
}
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  color: #2c3e50;
  margin-top: 60px;
}
.brand-danger {
  background-color: #d9534f !important;
  color: white !important ;
}
.brand-warning {
  background-color: #f0ad4e !important;
  color: white !important ;
}
.brand-primary {
  background-color: #337ab7 !important;
  color: white !important ;
}
.brand-success {
  background-color: #5cb85c !important;
  color: white !important ;
}
.panel {
  border: none;
  -webkit-box-shadow: 0 1px 1px rgba(0, 0, 0, .3);
  box-shadow: 0 1px 1px rgba(0, 0, 0, .3);
}
</style>
