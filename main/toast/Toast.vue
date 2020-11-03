<template>
<div class="toast" v-show="isShow">
<div class="mes">{{message}}</div>
</div>
</template>

<script>
export default {
  name: "Toast",
  data(){
    return{
      message:'',
      isShow:false
    }
  },
  methods:{
    show(message,duration=2000){
      this.message = message
      this.isShow = true
      setTimeout(()=>{
        this.isShow = false
        this.message = ''
      },duration)
    }
  }
}
</script>

<style scoped>
.toast{
  position: absolute;
  top: 50%;
  left: 50%;
  transform: translate(-50%,-50%);
  padding: 8px 10px;
  z-index: 999;
  color:#fff;
  background-color: rgba(0,0,0,.75);
  display: inline-block;
}
.mes{
  word-break:keep-all;
  /*white-space:nowrap;*/
}
</style>