<template>
  <div id="app">
    <router-view v-slot="{ Component }">
      <keep-alive exclude="Detail">
        <component :is="Component" />
      </keep-alive>
    </router-view>
    <main-tar-bar></main-tar-bar>
  </div>
</template>

<script>
// import MainTarBar from '../../components/content/maintarbar/MainTarBar.vue'
import MainTarBar from "../src/components/content/maintarbar/MainTarBar";

export default {
  name: "app",
  components: {
    MainTarBar,
  },
};
</script>

<style>
@import "./assets/css/base.css";
</style>
