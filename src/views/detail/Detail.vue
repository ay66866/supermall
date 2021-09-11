<!--  -->
<template>
  <div id="detail">
    <detail-nav-bar/>
    <detail-swiper  :top-images="topImages" />
  </div>
</template>

<script>
import DetailNavBar from './childComps/DetailNavBar.vue'
import DetailSwiper from './childComps/DetailSwiper.vue'

import {getDetail} from '../../network/detail'

export default {
  name: 'Detail',
  components: {
    DetailNavBar,
    DetailSwiper
  },
  data() {
    return {
      iid:null,
      topImages: []
    }
  },
  created() {
    // 保存存入的iid
    this.iid = this.$route.params.iid
    
    // 根据iid请求详情数据
    getDetail(this.iid).then(res => {
      this.topImages = res.result.itemInfo.topImages
    })
  }
}

</script>
<style >
</style>