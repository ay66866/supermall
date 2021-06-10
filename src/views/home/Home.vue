<template>
  <div>
    <nav-bar class="home-nav">
      <template v-slot:center>购物街</template>
    </nav-bar>
  </div>
</template>

<script>
import NavBar from '../../components/common/navbar/NavBar.vue';
import {getHomeMultidata} from "../../network/request"

export default {
  name: "Home",
  components: {
    NavBar,getHomeMultidata
  },
};
</script>


<style>
.home-nav {
  background-color: var(--color-tint);
  color:#fff
}
</style>
