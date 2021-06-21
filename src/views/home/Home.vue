<template>
  <div>
    <nav-bar class="home-nav">
      <template v-slot:center>购物街</template>
    </nav-bar>
    <home-swiper :banners="banners" />
  </div>
</template>

<script>
import NavBar from "components/common/navbar/NavBar.vue";
import HomeSwiper from "./childComps/HomeSwiper";

import { getHomeMultidata } from "../../network/home";
// import Swiper from '../../components/common/swiper/Swiper.vue';
// import SwiperItem from '../../components/common/swiper/SwiperItem.vue'

export default {
  name: "Home",
  components: {
    NavBar,
    HomeSwiper,
  },
  data() {
    return {
      banners: [],
      recommends: [],
    };
  },
  created() {
    getHomeMultidata().then((res) => {
      this.banners = res.data.banner.list;
      this.recommends = res.data.recommend.list;
    });
  },
};
</script>


<style>
.home-nav {
  background-color: var(--color-tint);
  color: #fff;
}
</style>
