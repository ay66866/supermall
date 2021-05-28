<template>
  <div>
    <tar-bar>
      <tar-bar-item path="/home">
          <template v-slot:item-icon>
            <img src="../../../assets/img/tabbar/home.svg" alt="">
          </template>
          <template v-slot:item-icon-active>
            <img src="../../../assets/img/tabbar/home_active.svg" alt="">
          </template>
          <template v-slot:item-text>
            <div>首页</div>
          </template>
        </tar-bar-item>
        <tar-bar-item path="/category">
          <template v-slot:item-icon>
            <img src="../../../assets/img/tabbar/category.svg" alt="">
          </template>
          <template v-slot:item-icon-active>
            <img src="../../../assets/img/tabbar/category_active.svg" alt="">
          </template>
          <template v-slot:item-text>
            <div>分类</div>
          </template>
        </tar-bar-item>
        <tar-bar-item path="/cart">
          <template v-slot:item-icon>
            <img src="../../../assets/img/tabbar/shopcart.svg" alt="">
          </template>
          <template v-slot:item-icon-active>
            <img src="../../../assets/img/tabbar/shopcart_active.svg" alt="">
          </template>
          <template v-slot:item-text>
            <div>购物车</div>
          </template>
        </tar-bar-item>
        <tar-bar-item path="/profile">
          <template v-slot:item-icon>
            <img src="../../../assets/img/tabbar/profile.svg" alt="">
          </template>
          <template v-slot:item-icon-active>
            <img src="../../../assets/img/tabbar/profile_active.svg" alt="">
          </template>
          <template v-slot:item-text>
            <div>我的</div>
          </template>
        </tar-bar-item>
      <!-- <tar-bar-item path="/home" >
        dom 中使用路径需要用 ~ 来识别配置的别名
        <img slot="item-icon" src="assets/img/tabbar/home.svg" alt="">
        <img slot="item-icon-active" src="assets/img/tabbar/home_active.svg" alt="">
        <div slot="item-text">首页</div>
      </tar-bar-item>
      <tar-bar-item path="/category">
        <img slot="item-icon" src="assets/img/tabbar/category.svg" alt="">
        <img slot="item-icon-active" src="assets/img/tabbar/category_active.svg" alt="">
        <div slot="item-text">品类</div>
      </tar-bar-item>
      <tar-bar-item path="/cart">
        <img slot="item-icon" src="assets/img/tabbar/shopcart.svg" alt="">
        <img slot="item-icon-active" src="assets/img/tabbar/shopcart_active.svg" alt="">
        <div slot="item-text">购物车</div>
      </tar-bar-item>
      <tar-bar-item path="/profile">

        <img slot="item-icon" src="assets/img/tabbar/profile.svg" alt="">
        <img slot="item-icon-active" src="assets/img/tabbar/profile_active.svg" alt="">
        <div slot="item-text">我的</div>
      </tar-bar-item> -->
    </tar-bar>
  </div>
</template>

<script>
    import TarBar from '../../common/tarbar/TarBar'
    import TarBarItem from '../../common/tarbar/TarBarItem'
    export default {
        name: "MainTarBar",
        components: {
            TarBar,
            TarBarItem
        }
    }
</script>

<style scoped>
.tar-bar-item img {
  width: 24px;
    height: 24px;
    vertical-align: middle;
    margin: 4px 0 2px 0;
}
</style>