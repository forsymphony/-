<template>
<div class="wrapper" ref="wrapper">
  <div class="content">
    <slot></slot>
  </div>
</div>
</template>

<script>
import BScroll from 'better-scroll'
export default {
  name: "Scroll",
  props:{
    //实时发送scroll
    probeType: {
      type:Number,
      default:0
    },
    //是否开启上拉加载
    pullUpLoad:{
      type:Boolean,
      default: false
    }
  },
  data(){
    return{
      //创建实例
      scroll:null
    }
  },

  mounted() {
    //新建scroll对象
      this.scroll = new BScroll(this.$refs.wrapper, {
        click:true,
        probeType:this.probeType,
        pullUpLoad:this.pullUpLoad
      })
    //监听滚动事件 并发射位置
    this.scroll.on('scroll',(position)=>{
      this.$emit('scroll',position)
    })
    //监听上拉事件 并发射
    this.scroll.on('pullingUp',()=>{
            this.$emit('pullingUp')
        })
    // this.scroll.scroll.refresh()
  },
  methods:{
    //定位
    scrollTo(x,y,time=300){
      this.scroll&&this.scroll.scrollTo(x,y,time)
    },
    //上拉刷新
    finishPullUp(){
      this.scroll&&this.scroll.finishPullUp()
    },
    //刷新
    refresh(){
      // console.log('111')
      this.scroll&&this.scroll.refresh()
    },
    //保存当前滚动到的位置
    getScrollY(){
      return this.scroll ? this.scroll.y : 0
    }

  }
}
</script>

<style scoped>
</style>
<!--基于better-scroll的滚动组件-->