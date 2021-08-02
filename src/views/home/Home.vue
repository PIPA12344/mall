<template>
  <div id="home">
    <nav-bar>
      <div slot="center">购物街</div>
    </nav-bar>
    <scroll class="content" ref="scroll" :probe-type="3" @scroll="scrollContent" :pull-up-load="true"
    @pullingUp="loadMore">
    <Home-swiper :banners="banners"></Home-swiper>
    <recommend-view :recommends="recommends">
    </recommend-view>
    <feature-view></feature-view>
    <tab-control :titles="titles" class="tab-control" @item-click="itemClick"></tab-control>
    <goods-list :goods="goods[type].list"></goods-list>
    </scroll>
    <back-top @click.native="backTopClick" v-show="isShow"></back-top>
  </div>
</template>
<script>
import NavBar from "@/components/common/navbar/NavBar";
import {getHomeMultidata} from "@/network/home";
import {getHomeGoods} from "@/network/home";
import HomeSwiper from "@/views/home/childComps/HomeSwiper";
import RecommendView from "@/views/home/childComps/RecommendView";
import FeatureView from "@/views/home/childComps/FeatureView";
import TabControl from "@/components/content/tabControl/TabControl";
import GoodsList from "@/components/content/goods/GoodsList";
import BackTop from "@/components/content/backTop/BackTop";
import Scroll from "@/components/common/scroll/Scroll";
export default {
  name: "Home",
  components: {
    NavBar,
    HomeSwiper,
    RecommendView,
    FeatureView,
    TabControl,
    GoodsList,
    BackTop,
    Scroll,
  },
  data() {
    return{
      banners: [],
      recommends: [],
      // result: null
      titles: ['流行','新款','精选'],
      goods: {
        'pop' :{page: 0,list: []},
        'new' :{page: 0,list: []},
        'sell' :{page: 0,list: []}
      },
      type: 'pop',
      isShow: false
    }
  },
  comments: {
    NavBar
  },
  created() {
    //1.请求多个数据
    this.getHomeMultidata()
    this.getHomeGoods('pop')
    this.getHomeGoods('new')
    this.getHomeGoods('sell')

    this.$bus.$on('imageLoad', () => {
      console.log("imageLoadComplete");
      this.$refs.scroll.refresh()
    })
  },
  methods: {
    itemClick(index) {
      if(index === 0) {
        this.type = 'pop'
      }
      else if(index === 1) {
        this.type = 'new'
      }
      else {
        this.type = 'sell'
      }
    },
    getHomeMultidata() {
      getHomeMultidata().then(res => {
        this.banners =res.data.banner.list
        this.recommends=res.data.recommend.list
      })
    },
    getHomeGoods(type){
      const page = this.goods[type].page+1
      getHomeGoods(type,page).then(res => {
        this.goods[type].list.push(...res.data.list)
        this.goods[type].page += 1
        this.$refs.scroll.finishPullUp()
      }
      )
    },
    backTopClick() {
      this.$refs.scroll.scrollTo()
    },
    scrollContent(position) {
      this.isShow = (-position.y) > 1000
    },
    loadMore() {
      this.getHomeGoods(this.type)
    },
  }
}
</script>

<style scoped>
  .nav-bar {
    text-align: center;
    background-color: pink;
    color: white;
  }
  .tab-control {
    position: sticky;
    top: 43px;
  }
  #home {
    height: 100vh;
  }
  .content {
    height: calc(100%  - 49px);
    overflow: hidden;
  }
</style>
