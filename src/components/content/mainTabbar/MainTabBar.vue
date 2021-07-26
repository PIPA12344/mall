<template>
  <tab-bar>
    <tab-bar-item link="/home">
      <img src="../../assets/img/TabBar/home.svg" alt=" " slot="item-icon">
      <img src="../../assets/img/TabBar/home_active.svg" alt=" " slot="item-icon-active">
      <div slot="item-text">首页</div>
    </tab-bar-item>
    <tab-bar-item link="/category">
      <img src="../../assets/img/TabBar/category.svg" alt=" " slot="item-icon">
      <img src="../../assets/img/TabBar/category_active.svg" alt=" " slot="item-icon-active">
      <div slot="item-text">分类</div>
    </tab-bar-item>
    <tab-bar-item link="/cartshop" active-color="deepPink">
      <img src="../../assets/img/TabBar/shopcart.svg" alt=" " slot="item-icon">
      <img src="../../assets/img/TabBar/shopcart_active.svg" alt=" " slot="item-icon-active">
      <div slot="item-text">购物车</div>
    </tab-bar-item>
    <tab-bar-item link="/profile">
      <img src="../../assets/img/TabBar/profile.svg" alt=" " slot="item-icon">
      <img src="../../assets/img/TabBar/profile_active.svg" alt=" " slot="item-icon-active">
      <div slot="item-text">我的</div>
    </tab-bar-item>
  </tab-bar>
</template>

<script>
import TabBar from "../tabbar/TabBar";
import TabBarItem from "../tabbar/TabBarItem";
export default {
  name: "MainTabBar",
  components: {
    TabBar,
    TabBarItem
  }
}
</script>

<style scoped>

</style>
