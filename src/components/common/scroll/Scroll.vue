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
BScroll.use(ObserveDom)


export default {
  name: "Scroll",
  props: {
    probeType: {
      type: Number,
      default: 0,
    }
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
      probeType: this.probeType
    }),
      // this.scroll.scrollTo(0, 0);
      this.scroll.on('scroll', (postion) => {
        this.$emit('scroll', postion)
      })
  },
  methods: {
    scrollTo(x, y, time = 300) {
      this.scroll.scrollTo(x, y, time);
    },
  },
};
</script>

<style>
</style>