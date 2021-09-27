<template>
  <div class="cart">
    <nav-bar class="nav-bar">
      <template v-slot:center>购物车({{ length }})</template>
    </nav-bar>
  </div>
</template>

<script>
import NavBar from "components/common/navbar/NavBar.vue";
import { useStore, mapGetters } from "vuex";


export default {
  name: "Cart",
  setup: function () {
    const store = new useStore();
    return {
      store,
    };
  },
  components: {
    NavBar,
  },
  computed: {
    ...mapGetters({
        length: 'cartLength',
        list: 'cartList'
    })
  },
};
</script>

<style scoped>
.nav-bar {
  background-color: var(--color-tint);
  color: #fff;
  /* font-weight: 700; */
}
</style>
