<template>
  <div class="wrapper" ref ="aaa">
    <div class="content">
      <slot></slot>
    </div>
  </div>
</template>

<script>
import BScroll from "better-scroll";
export default {
  name: "Scroll",
  data() {
    return{
      scroll: null,
    }
  },
  props: {
    probeType: 0,
    pullUpLoad: {
      type: Boolean,
      default: false
    }
  },
  mounted() {
    this.scroll = new BScroll(this.$refs.aaa,{
      click: true,
      probeType: this.probeType,
      pullUpLoad: this.pullUpLoad
    })
    this.scroll.on('scroll',(position) => {
      // console.log(position);
      this.$emit("scroll",position)
    })
    this.scroll.on('pullingUp',() => {
      this.$emit('pullingUp')
    })
    console.log(this.scroll);
  },
  methods: {
    scrollTo (x=0,y=0,time = 500) {
      this.scroll.scrollTo(x,y,time)
    },
    finishPullUp() {
      this.scroll.finishPullUp()
    },
    refresh() {
      this.scroll.refresh()
    }

  }
}
</script>

<style scoped>
  .wrapper {
    height: 100%;
  }
</style>
