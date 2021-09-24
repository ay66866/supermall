<template>
  <div class="wrapper" ref="wrapper">
    <div class="content">
      <slot></slot>
    </div>
  </div>
</template>

<script>
import BScroll from "better-scroll";
import ObserveDom from "@better-scroll/observe-dom"
import Pullup from "@better-scroll/pull-up"

BScroll.use(ObserveDom)
BScroll.use(Pullup)


export default {
  name: "Scroll",
  props: {
    probeType: {
      type: Number,
      default: 0,
    },
    pullUpLoad: {
      type: Boolean,
      default: false
    },
  },
  
  data() {
    return {
      scroll: null,
    };
  },
  mounted() {
    // 1.创建scroll对象
    this.scroll = new BScroll(this.$refs.wrapper, {
      click: true,
      observeDOM: true,
      // observeImage: true,
      observeImage: {debounceTime: 300},                                                                                                                                                                                                
      probeType: this.probeType,  
      pullUpLoad: true,    
      // momentum: true,
      deceleration: 0.001

    }),
    // 2.监听滚动对象
      // this.scroll.scrollTo(0, 0);
    
      this.scroll.on('scroll', (position) => {
        this.$emit('scroll', position)
      })
    
      // 3.监听上拉事件
    this.scroll.on('pullingUp', ()=>{
      this.$emit('pullingUp')
    })
  },      
  methods: {
    scrollTo(x, y, time = 300) {
      this.scroll.scrollTo(x, y, time);
    },
    finishPullUp() {
      this.scroll.finishPullUp()
    },
    refresh() {
      this.scroll && this.scroll.refresh()
    },
    getScrollY() {
      return this.scroll ? this.scroll.y : 0 
    },
  },
};
</script>

<style>
</style>