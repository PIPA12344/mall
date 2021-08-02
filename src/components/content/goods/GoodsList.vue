<template>
  <div class="goods">
    <goods-item v-for="item in goods" :goodsItem="item"/>
  </div>
</template>

<script>
import GoodsItem from "@/components/content/goods/GoodsItem";
export default {
  name: "GoodsList",
  props: {
    goods: {
      type: Array,
      default() {
        return []
      }
    }
  },
  components: {
    GoodsItem
  }
}
</script>

<style scoped>
  .goods {
    display: flex;
    justify-content: space-around;
    flex-wrap: wrap;
  }
</style>
