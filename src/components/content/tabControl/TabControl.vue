<template>
  <div class="tab-control">
    <div v-for="(item,index) in titles"
         class="tab-control-item"
         :class="{active:index===currentIndex}"
         @click="itemClick(index)">
      <span>{{item}}</span>
    </div>
  </div>
</template>

<script>
import TabBarItem from "@/components/common/tabbar/TabBarItem";
export default {
  name: "TabControl",
  components: {TabBarItem},
  data() {
    return {
      currentIndex : 0
    }
  },
  props: {
    titles : {
      type: Array,
      default() {
        return [];
      }
    }
  },
  methods: {
    itemClick(index) {
      this.currentIndex=index
      this.$emit("item-click",index)
    }
  }
}
</script>

<style scoped>
  .tab-control {
    display: flex;
    width: 100%;
    text-align: center;
    height: 40px;
    background-color: white;
  }
  .tab-control-item {
    flex: 1;
    line-height: 40px;
    font-size: 15px;
    height: 40px;
  }
  .active {
    color: red;
    border-bottom: 3px solid red;
  }

</style>
