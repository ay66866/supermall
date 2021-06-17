<template>
  <div>
    <nav-bar class="home-nav">
      <template v-slot:center>购物街</template>
    </nav-bar>            
    <swiper>
      <swiper-item v-for="item in banners" :key="item.index">
        <a :href="item.link">
          <img :src="item.image" alt="">
        </a>
      </swiper-item>
    </swiper>
  </div>
</template>

<script>
import NavBar from "../../components/common/navbar/NavBar.vue";
import { getHomeMultidata } from "../../network/home";
// import Swiper from '../../components/common/swiper/Swiper.vue';
// import SwiperItem from '../../components/common/swiper/SwiperItem.vue'
import { Swiper, SwiperItem } from "../../components/common/swiper";  

export default {
  name: "Home",
  components: {
    NavBar,
    Swiper,
    SwiperItem
  },
  data() {
    return {
      banner: [],
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
