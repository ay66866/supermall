<template>
  <div id="app">
    <main-tar-bar/>
  </div>
</template>

<script>
  import MainTarBar from 'components/content/maintarbar/MainTarBar.vue'

  export default {
    name: "app",
    components: {
      MainTarBar
    },
  };
</script>

<style>
  @import "assets/css/base.css";
</style>
