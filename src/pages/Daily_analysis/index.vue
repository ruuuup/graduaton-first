<template>
  <div id="wrap">
    <div id="top">
      <img src="../../../static/images/analysisbg.jpeg" alt="" style="width: 100%; height: 100vh;">
      <div id="center">
        <i-button @click="toggleLeft1">运动日</i-button>
        <i-button @click="toggleRight1">非运动日</i-button>
      </div>
    </div>

  </div>
</template>
<script>
  export default {
    data(){
      return{

      }
    },
    methods:{
      toggleLeft1() {

      },
      toggleRight1(){

      }
    }
  }
</script>
<style scoped>
  #wrap{
    width: 100%;
    height: 100vh;
  }
  #top{
    position: relative;
  }
  #top #center{
    width: 100%;
    position: absolute;
    left: 1%;
    top:30%;
  }
  .btn1{
    color:yellow !important;
  }
  .echarts-wrap {
    width: 100%;
    height: 300px;
  }

</style>










