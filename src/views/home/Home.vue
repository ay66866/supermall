<template>
  <div id="home">
    <nav-bar class="home-nav">
      <template v-slot:center>购物街</template> 
    </nav-bar>
    <tab-control     
      :titles="['流行', '新款', '精选']"    
      @tabClick="tabClick"
      ref="tabControl1"
      class="tab-control"
      v-show="isTabFixed"
    />
    <scroll
      class="content"
      ref="scroll"
      :probe-type="3"
      @scroll="contentScroll"
      :pull-up-load="true"
      @pullingUp="loadMore"
    >
      <home-swiper :banners="banners" @swiperImageLoad="swiperImageLoad" />
      <recommend-view :recommends="recommends" />
      <feature-view />
      <tab-control
        :titles="['流行', '新款', '精选']"    
        @tabClick="tabClick"
        ref="tabControl2"
      />
      <goods-list :goods="goods[currentType].list" />
    </scroll>
    <back-top @click="backClick" v-show="isShowBackTop" />
  </div>
</template>

<script>
import NavBar from "components/common/navbar/NavBar.vue";
import TabControl from "components/content/tabControl/TabControl";
import GoodsList from "components/content/goods/GoodsList.vue";
import Scroll from "components/common/scroll/Scroll.vue";
// import BackTop from "components/content/backTop/BackTop";

import HomeSwiper from "./childComps/HomeSwiper";
import RecommendView from "./childComps/RecommendView.vue";
import FeatureView from "./childComps/FeatureView.vue";

import { getHomeMultidata, getHomeGoods } from "../../network/home";
import { backTopMixin } from "../../../common/mixin";

// import Swiper from '../../components/common/swiper/Swiper.vue';
// import SwiperItem from '../../components/common/swiper/SwiperItem.vue'

export default {
  name: "Home",
  components: {
    NavBar,
    TabControl,
    HomeSwiper,
    RecommendView,
    FeatureView,
    GoodsList,
    Scroll,
    // BackTop,
  },
  mixins: [backTopMixin],
  data() {
    return {
      banners: [],
      recommends: [],
      goods: {
        pop: { page: 0, list: [] },
        new: { page: 0, list: [] },
        sell: { page: 0, list: [] },
      },
      currentType: "pop",
      isShowBackTop: false,
      // tabOffsetTop: 0,
      isTabFixed: false,
      saveY: 0
    };
  },
    activated() { 
      this.$refs.scroll.refresh()
      this.$refs.scroll.scrollTo(0, this.saveY, 0)  
    },
    deactivated() {
      this.saveY = this.$refs.scroll.getScrollY()
    },
  created() {
    // 1.请求多个数据
    this.getHomeMultidata();

    // 2.请求商品数据
    this.getHomeGoods("pop");
    this.getHomeGoods("new");
    this.getHomeGoods("sell");
    
  },
//   mounted() {
//  // 3.监听item中图片加载完成
//     Bus.$on('itemImageLoad', () => {
//       this.$refs.scroll.scroll.refresh()
//     })
//   },
  methods: {
    // 时间监听
    tabClick(index) {
      switch (index) {
        case 0:
          this.currentType = "pop";
          break;
        case 1:
          this.currentType = "new";
          break;
        case 2:
          this.currentType = "sell";
          break;
      }
      this.$refs.tabControl1.currentIndex = index;
      this.$refs.tabControl2.currentIndex = index;
    },
    backClick() {
      this.$refs.scroll.scrollTo(0, 0);
      
    },
    loadmore() {
      this.getHomeGoods(this.currentType);
      this.$refs.scroll.scroll.refresh()
    },
    contentScroll(position) {
      // console.log(postion);
      // 1.判断BackTop
      this.listenShowBackTop(position)
      // this.isShowBackTop = -position.y > 1000; 
      //2.判断tabControl是否吸顶
      this.isTabFixed = (-position.y) > this.tabOffsetTop
    },
    loadMore() {
      this.getHomeGoods(this.currentType)
    },
    swiperImageLoad() {
      this.tabOffsetTop = this.$refs.tabControl2.$el.offsetTop;
    },
    //网络请求相关
    getHomeMultidata() {
      getHomeMultidata().then((res) => {
        this.banners = res.data.banner.list;
        this.recommends = res.data.recommend.list;
      });
    },
    getHomeGoods(type) {
      const page = this.goods[type].page + 1;
      getHomeGoods(type, page).then(res => {
        this.goods[type].list.push(...res.data.list);
        this.goods[type].page+=1;
        this.$refs.scroll.finishPullUp()
      });
    },
  },
};
</script>


<style scoped>
#home {
  position: relative;
  /* padding-top: 44px; */
  height: 100vh;
}
.home-nav {
  background-color: var(--color-tint);
  color: #fff;
  /* position: fixed;
  left: 0;
  right: 0;
  top: 0;
  z-index: 9; */
}
/* .tab-control {
  position: sticky;
  top: 44px;
  z-index: 9;
} */
.content {
  overflow: hidden;
  position: absolute;
  top: 44px;
  bottom: 49px;
  right: 0;
  left: 0;
}
.tab-control {
  position: relative;
  z-index: 9;
}
/* .fixed {
  position: fixed;
  left: 0;
  right: 0;
  top: 44px;
} */
/* .content {         
  height: calc(100% - 93px);
  overflow: hidden;
  margin-top: 44px;
} */
</style>
