<template>
  <div id="wrap">
    <text class="title">通过图表实时观察您的体重趋势</text>
    <div class="echarts-wrap">
      <mpvue-echarts :echarts="echarts" :onInit="onInit" canvasId="demo-canvas" />
    </div>
    <button @click="handleOpen1">记录体重</button>
    <i-modal title="今日体重" :visible="visible1" @ok="recordweight" @cancel="handleClose1">
      <text>{{testdate}}</text>
      <input type="text" v-modal="test" @change="inputchange" placeholder="请输入体重(公斤)"/>
    </i-modal>
  </div>

</template>
<script>
  import echarts from 'echarts'
  import mpvueEcharts from 'mpvue-echarts'
  let chart=null
  function initChart(canvas, width, height) {
    chart = echarts.init(canvas, null, {
      width: width,
      height: height
    });
    canvas.setChart(chart);

    var option = {
      title: {
        // text: '未来一周气温变化',
        subtext: '单位公斤'
      },
      xAxis: {
        type: 'category',
        boundaryGap: false,
        data: []
      },
      yAxis: {
        type: 'value'
      },
      series: [{
        data: [],
        type: 'line',
        areaStyle: {}
      }]
    }; // ECharts 配置项

    chart.setOption(option);

    // return chart; // 返回 chart 后可以自动绑定触摸操作
  }
  export default {
    components:{
      mpvueEcharts
    },
    data(){
      return{
        echarts,
        onInit: initChart,
        test:"",
        arrx:[],
        arry:[],
        visible1: false,
        testdate:""
      }
    },
    computed:{
      testdate:function() {
        return new Date();
      }
    },
    methods:{
      recordweight(){
        this.visible1=false;
        var option = {
          title: {
            // text: '未来一周气温变化',
            subtext: '单位公斤'
          },
          xAxis: {
            type: 'category',
            boundaryGap: false,
             data: this.arrx


          },
          yAxis: {
            type: 'value',
            // axisLabel: {
            //   formatter: '{value}公斤'
            // }

          },
          series: [{
            data: this.arry,
            type: 'line',
            areaStyle: {}
          }]
        };
        console.log("====="+chart.getOption().xAxis[0].data);
        console.log("====="+chart.getOption().yAxis[0].data);
       console.log("###"+this.test);
        this.arry.push(this.test);
        this.arrx.push(this.testdate);
        chart.setOption(option)
      },
      inputchange(e){
        console.log("9999"+e.mp.detail.value);
        this.test=e.mp.detail.value
      },
      handleOpen1 () {
        this.visible1=true;
      },
      handleClose1(){
        this.visible1=false;
      }
    },
    created:function() {
      console.log("kkkk"+JSON.stringify(mpvueEcharts));
      var date=new Date();
      let year=date.getFullYear();
      let month=date.getMonth()+1;
      let day=date.getDate();
      this.testdate=year+'/'+month+'/'+day;
    }
  }

</script>
<style scoped>
  .echarts-wrap {
    width: 100%;
    height: 300px;
  }
  input{
    border: 1px solid lightgray;
    width: 80%;
    margin: 0 auto;
    border-radius: 10px;
    height:40px;
  }
  button{
    background-color: #2db7f5;
    color: white;
  }
  .title{
    margin-left: 30%;
    font-size: 12px;
    color: gray;
  }
</style>
