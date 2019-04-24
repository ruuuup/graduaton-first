<template>
    <div id="wrap">
      <div id="top">
        <mpvue-echarts :echarts="echarts" :onInit="onInit" canvasId="demo-canvas" />
      </div>
      <div id="content">
          <i-panel v-if="listwmorning.length>0"  title="早餐(建议364-445千卡)" i-class="title">
            <i-cell  v-for="(item,index) in listwmorning" :title="item.name"  is-link>{{item.pical}}千卡/100克
              <i-icon @click.stop="missmorning(item,index)"  type="delete" color="orange" size="20"/>
            </i-cell>
          </i-panel>

        <i-panel v-if="listwnoon.length>0" title="午餐(建议486-594千卡)">
          <i-cell  v-for="item in listwnoon" title="只显示箭头" :title="item.name"  is-link>{{item.pical}}千卡/100克
            <i-icon @click.stop="missnoon(item,index)"  type="delete" color="orange" size="20"/>
          </i-cell>
        </i-panel>
        <i-panel v-if="listwafternoon.length>0" title="晚餐(建议364-445千卡)">
          <i-cell  v-for="item in listwafternoon" title="只显示箭头" :title="item.name"  is-link>{{item.pical}}千卡/100克
            <i-icon @click.stop="missafternoon(item,index)"  type="delete" color="orange" size="20"/>
          </i-cell>
        </i-panel>
        <!--<i-modal title="添加克数" :visible="visible1" @ok="okcan()" @cancel="cancelcan()">-->
          <!--<input type="text" @change="inputchange" placeholder="请输入克数"/>-->
        <!--</i-modal>-->
        <i-panel v-if="listsport.length>0" title="运动">
          <i-cell  v-for="item in listsport" title="只显示箭头" :title="item.name" is-link>{{item.pical}}千卡/小时</i-cell>
        </i-panel>
      </div>
      <!--<modal v-if="hiddenmodalput" title="请填写克数" confirm-text="确定" cancel-text="取消" @cancel="cancelM" @confirm="confirmM">-->
        <!--<input type="text" @change="inputchange2" style="border: 1px solid lightgray;">-->
      <!--</modal>-->
      <!--<button @click="an()">按我</button>-->
      <div id="footer">
        <!--<button class="btn">每日分析</button>-->
        <ul>
          <li @click="toSearch('morning')"><i class="icon iconfont icon-zaocan"></i><text>早餐</text></li>
          <li @click="toSearch('noon')"><i class="icon iconfont icon-wucan"></i><text>午餐</text></li>
          <li @click="toSearch('night')"><i class="icon iconfont icon-wancan"></i><text>晚餐</text></li>
          <li @click="toSport('sport')"><i class="icon iconfont icon-yundong"></i><text>运动</text></li>
        </ul>
      </div>
    </div>
</template>
<script>
  import echarts from 'echarts'
  import mpvueEcharts from 'mpvue-echarts'
  let chart=null
  var count=0
  // console.log()
  // console.log("总卡"+ this.globalData.allcal);
  function initChart(canvas, width, height){
    chart = echarts.init(canvas, null, {
      width: width,
      height: height
    });
    canvas.setChart(chart);

   var option = {
      tooltip: {
        trigger: 'item',
        formatter: "{a} <br/>{b}: {c} ({d}%)"
      },
      legend: {
        orient: 'vertical',
        x: 'left',
        data:['每日可摄入量','今日摄入量']
      },
      series: [
        {
          name:'访问来源',
          type:'pie',
          radius: ['50%', '70%'],
          avoidLabelOverlap: false,
          label: {
            normal: {
              show: false,
              position: 'center'
            },
            emphasis: {
              show: true,
              textStyle: {
                fontSize: '30',
                fontWeight: 'bold'
              }
            }
          },
          labelLine: {
            normal: {
              show: false
            }
          },
          data:[
            {value:1351, name:'每日可摄入量'},
            {value:count, name:'今日摄入量'},

          ]
        }
      ],
      color:["lightblue","orange"]
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
        // hiddenmodalput:false,
        itemadd:{},
        can:'',
        // addcal:"",
        // visible1:false,
        echarts,
        onInit: initChart,
        out:"33",
        current: 'tab1',
        listwmorning:[],
        listwnoon:[],
        listwafternoon:[],
        listsport:[],
        personrecord:[
          {date:"2019/4/16",morningintake:[{name:"全麦面包",cal:"200大卡"}],overalltake:"3800"}
        ]
        // current_scroll: 'tab1'
      }
    },
    methods:{
      // an(){
      //   this.listwmorning[0].pical=200;
      // },
      // inputchange2(e){
      //   this.addcal=e.mp.detail.value;
      // },
      // cancelM(){
      //   this.hiddenmodalput=false;
      // },
      // confirmM(){
      //   this.hiddenmodalput=false;
      //   this.itemadd.pical=(parseInt(this.addcal)/100)*parseInt(this.itemadd.pical);
      // },
      toSearch(key){
       wx.navigateTo({
         url:"../Search_food/main?key="+key
       })
      },
      toSport(){
        wx.navigateTo({
          url:"../Daily_sports/main"
        })
      },
      // okcan(){
      //   this.visible1=false;
      // },
      // cancelcan(){
      //   this.visible1=true;
      // },
      // inputchange(e){
      //   this.can=e.mp.detail.value;
      // },
      // handleChange ({ detail }) {
      //   this.setData({
      //     current: detail.key
      //   });
      // },
      missmorning(item,index){
        wx.showModal({
          title:"提示",
          content:"确定将该食材从今日饮食中删除么",
          success:res=>{
            if(res.confirm){
              this.listwmorning.splice(index,1);
              this.globalData.listmorning.splice(index,1);
              this.globalData.allcal=this.globalData.allcal-parseInt(item.pical);
              var option = {
                tooltip: {
                  trigger: 'item',
                  formatter: "{a} <br/>{b}: {c} ({d}%)"
                },
                legend: {
                  orient: 'vertical',
                  x: 'left',
                  data:['每日可摄入量','今日摄入量']
                },
                series: [
                  {
                    name:'访问来源',
                    type:'pie',
                    radius: ['50%', '70%'],
                    avoidLabelOverlap: false,
                    label: {
                      normal: {
                        show: false,
                        position: 'center'
                      },
                      emphasis: {
                        show: true,
                        textStyle: {
                          fontSize: '30',
                          fontWeight: 'bold'
                        }
                      }
                    },
                    labelLine: {
                      normal: {
                        show: false
                      }
                    },
                    data:[
                      {value:1351, name:'每日可摄入量'},
                      {value:this.globalData.allcal, name:'今日摄入量'},

                    ]
                  }
                ],
                color:["lightblue","orange"]
              }; // ECharts 配置项

              chart.setOption(option);
            }
          }
        })

      },
      missnoon(item,index){
        wx.showModal({
          title:"提示",
          content:"确定将该食材从今日饮食中删除么",
          success:res=>{
            if(res.confirm){
              this.listwnoon.splice(index,1);
              this.globalData.listnoon.splice(index,1);
              this.globalData.allcal=this.globalData.allcal-parseInt(item.pical);
              var option = {
                tooltip: {
                  trigger: 'item',
                  formatter: "{a} <br/>{b}: {c} ({d}%)"
                },
                legend: {
                  orient: 'vertical',
                  x: 'left',
                  data:['每日可摄入量','今日摄入量']
                },
                series: [
                  {
                    name:'访问来源',
                    type:'pie',
                    radius: ['50%', '70%'],
                    avoidLabelOverlap: false,
                    label: {
                      normal: {
                        show: false,
                        position: 'center'
                      },
                      emphasis: {
                        show: true,
                        textStyle: {
                          fontSize: '30',
                          fontWeight: 'bold'
                        }
                      }
                    },
                    labelLine: {
                      normal: {
                        show: false
                      }
                    },
                    data:[
                      {value:1351, name:'每日可摄入量'},
                      {value:this.globalData.allcal, name:'今日摄入量'},

                    ]
                  }
                ],
                color:["lightblue","orange"]
              }; // ECharts 配置项

              chart.setOption(option);
            }
          }
        })
      },
      missafternoon(item,index){
        wx.showModal({
          title:"提示",
          content:"确定将该食材从今日饮食中删除么",
          success:res=>{
            if(res.confirm){
              this.listwafternoon.splice(index,1);
              this.globalData.listafternoon.splice(index,1);
              this.globalData.allcal=this.globalData.allcal-parseInt(item.pical);
              var option = {
                tooltip: {
                  trigger: 'item',
                  formatter: "{a} <br/>{b}: {c} ({d}%)"
                },
                legend: {
                  orient: 'vertical',
                  x: 'left',
                  data:['每日可摄入量','今日摄入量']
                },
                series: [
                  {
                    name:'访问来源',
                    type:'pie',
                    radius: ['50%', '70%'],
                    avoidLabelOverlap: false,
                    label: {
                      normal: {
                        show: false,
                        position: 'center'
                      },
                      emphasis: {
                        show: true,
                        textStyle: {
                          fontSize: '30',
                          fontWeight: 'bold'
                        }
                      }
                    },
                    labelLine: {
                      normal: {
                        show: false
                      }
                    },
                    data:[
                      {value:1351, name:'每日可摄入量'},
                      {value:this.globalData.allcal, name:'今日摄入量'},

                    ]
                  }
                ],
                color:["lightblue","orange"]
              }; // ECharts 配置项

              chart.setOption(option);
            }
          }
        })
      },
      // addkil(item,index){
      //   this.hiddenmodalput=true;
      //   this.itemadd=item;
      // }
    },
    created(){

      var date =new Date();
      var year=date.getFullYear();
      var month=date.getMonth()+1;
      var day=date.getDate();
      let testdate=year+'/'+month+'/'+day;
      //根据当前系统的时间从缓存里拿到数据
      // count=this.globalData.allcal || 0;
      // console.log("ppp");
      console.log("1200");
    },
    onLoad(){

    },
    onShow(){
      this.globalData.allcal=this.globalData.allcal || 0;
      count=this.globalData.allcal;
      console.log("要死"+this.globalData.allcal);
      let listwmorning = this.globalData.listmorning || [];
      let listwnoon=this.globalData.listnoon || [];
      let listwafternoon=this.globalData.listafternoon || [];
      let listsport=this.globalData.sport || [];
      if(listwmorning.length>0){
        this.listwmorning=[];
        listwmorning.filter(value => {
          this.listwmorning.push({name:value.name,pical:value.cal});
        })
        this.listwmorning[this.listwmorning.length-1].pical=this.globalData.vcal;
      }
      if(listwnoon.length>0){
        this.listwnoon=[];
        listwnoon.filter(value => {
          this.listwnoon.push({name:value.name,pical:value.cal});
        })
        this.listwnoon[this.listwnoon.length-1].pical=this.globalData.vcal;
      }
      if(listwafternoon.length>0){
        this.listwafternoon=[];
        listwafternoon.filter(value => {
          this.listwafternoon.push({name:value.name,pical:value.cal});
        })
        this.listwafternoon[this.listwafternoon.length-1].pical=this.globalData.vcal;
      }
      if(listsport.length>0){
        this.listsport=[];
        listsport.filter(value => {
          this.listsport.push({name:value.title,pical:value.cal});
        })
        this.listsport[this.listsport.length-1].pical=this.globalData.scal;
      }

      console.log("morning"+JSON.stringify(this.listwmorning));

    }
  }

</script>
<style scoped>
  title{
    color: orange;
  }
  #wrap{
    width: 100%;
    height: auto;
  }
  #wrap #top{
    width: 100%;
    height: 280px;

    /*display: flex;*/

  }
  #wrap #top text{
    font-size: 12px;
  }
  #content{
    width: 100%;
    height: auto;
    margin-bottom: 80px;
  }
  #content .list{
    height: 40px;
    text-align: center;
    line-height: 40px;

  }
  #footer{

    width: 100%;
    height: 40px;
    position: fixed;
    left: 0;
    bottom: 0;
    z-index: 100;
    background: white;
  }
  #footer ul{
    width: 100%;
    display: flex;
  }
  #footer ul li{
    width: 25%;
    text-align: center;
    display: flex;
    flex-direction: column;
  }
  #footer ul li text{
    color: gray;
    font-size: 14px;
  }
  #footer ul li .icon-zaocan{
    color: orange;
  }
  #footer ul li .icon-wucan{
    color: lightgreen;
  }
  #footer ul li .icon-wancan{
    color: deepskyblue;
  }
  #footer ul li .icon-yundong{
    color: pink;
  }
</style>
