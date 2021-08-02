<template>
  <div class="goods-item">
    <div>
      <img :src="goodsItem.show.img" alt="" @load="imageLoad">
    </div>
    <div class="item-font">
      <p>{{goodsItem.title}}</p>
      <span class="price">￥{{goodsItem.price}}</span>
      <span class="cfav">⭐{{goodsItem.cfav}}</span>
    </div>
  </div>
</template>

<script>
export default {
  name: "GoodsItem",
  props: {
    goodsItem: {
      type: Object,
      default(){
        return {}
      }
    }
  },
  methods: {
    imageLoad() {
      this.$bus.$emit('imageLoad')
    }
  }
}
</script>

<style scoped>
  .goods-item {
    display: flex;
    width: 40%;
    flex-direction: column;
    justify-content: space-between;

  }
  .goods-item a{
    width: 100%;
  }
  .goods-item img {
    width: 100%;
  }
  .goods-item p {
    margin-left: 2px;
    overflow: hidden;
    text-overflow: ellipsis;
    white-space: nowrap;
    width: 100%;
  }
  .price {
    color: red;
  }
  .item-font {
    text-align: center;
    bottom:0;
    padding:0;
    margin-bottom: 3px;
  }
</style>
