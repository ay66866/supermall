<!--  -->
<template>
  <div>
    <nav-bar>
      <template  v-slot:left >
        <div @click="backClick">
         <img src="~@/assets/img/common/back.svg" alt="" />
        </div>
      </template>
      <template v-slot:center>
        <div
          v-for="(item, index) in titles"
          class="title-item"
          :key="item"
          :class="{ active: index === currentIndex }"
          @click="titleClick(index)"
        >
          {{ item }}
        </div>
      </template>
    </nav-bar>
  </div>
</template>
  
<script>
import NavBar from "components/common/navbar/NavBar.vue";

export default {
  name: "DetailNavBar",
  components: {
    NavBar,
  },
  data() {
    return {
      titles: ["商品", "参数", "评论", "推荐"],
      currentIndex: 0,
    };
  },
  methods: {
    titleClick(index) {
      this.currentIndex = index;
    },
    backClick() {
      this.$router.back()
    }
  },
};
</script>
<style>
.center {
  display: flex;
  font-size: 13px;
}
.title-item {
  flex: 1;
}
.left img {
  margin-top: 12px;
}
.active {
  color: var(--color-high-text);
}
</style>