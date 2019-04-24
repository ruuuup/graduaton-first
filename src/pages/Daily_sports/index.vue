<template>
  <div id="wrap">
    <div id="top">
      <i-cell-group>
          <i-cell @click="detail(item,index)" v-for="(item,index) in list" :title="item.title" is-link>{{item.cal}}千卡/小时
            <i-icon slot="icon" size="30" type="emoji" :color="item.color"></i-icon>
          </i-cell>

      </i-cell-group>
      <modal v-if="hiddenmodalsport" title="请填写小时数" confirm-text="确定" cancel-text="取消" @cancel="cancelM" @confirm="confirmM">
        <input type="text" @change="inputchange" style="border: 1px solid lightgray;">
      </modal>
    </div>
  </div>
</template>
<script>
  export default{
    data(){
      return{
        sportcal:"",
        hiddenmodalsport:false,
        sportitem:{},
        sportlist:[],
        list:[
          {
            title:"走路(慢)",
            cal:"95",
            color:"blue"
          },
          {
            title:"走路(快)",
            cal:"292",
            color:"yellow"
          },
          {
            title:"跑步(慢)",
            cal:"401",
            color:"red"
          },
          {
            title:"跑步(快)",
            cal:"554",
            color:"orange"
          },
          {
            title:"爬楼梯",
            cal:"394",
            color:"orange"
          },
          {
            title:"跳绳",
            cal:"423",
            color:"orange"
          },
          {
            title:"游泳",
            cal:"401",
            color:"orange"
          },
          {
            title:"自行车",
            cal:"423",
            color:"purple"
          },
          {
            title:"舞蹈，健身操",
            cal:"364",
            color:"purple"
          },
          {
            title:"踏板操",
            cal:"474",
            color:"green"
          },
          {
            title:"瑜伽，普拉提",
            cal:"146",
            color:"lightgreen"
          },
          {
            title:"茉雅减肥操",
            cal:"364",
            color:"green"
          },
          {
            title:"BodyJam58",
            cal:"386",
            color:"lightgreen"
          },
          {
            title:"Pump2004",
            cal:"364",
            color:"red"
          },
          {
            title:"Kitty(中极版)",
            cal:"364",
            color:"pink"
          },
          {
            title:"郑多燕(小红帽版)",
            cal:"233",
            color:"black"
          },
          {
            title:"篮球",
            cal:"401",
            color:"gray"
          },
          {
            title:"足球",
            cal:"437",
            color:"purple"
          },
          {
            title:"排球",
            cal:"343",
            color:"orange"
          },
          {
            title:"乒乓球",
            cal:"219",
            color:"green"
          },
          {
            title:"羽毛球",
            cal:"328",
            color:"brown"
          },
          {
            title:"网球",
            cal:"292",
            color:"yellow"
          },
          {
            title:"壁球",
            cal:"437",
            color:"black"
          },
          {
            title:"橄榄球",
            cal:"386",
            color:"pink"
          },
          {
            title:"垒球，棒球",
            cal:"219",
            color:"green"
          },
          {
            title:"曲棍球",
            cal:"496",
            color:"red"
          },
          {
            title:"攀岩，爬山",
            cal:"620",
            color:"yellow"
          },
          {
            title:"滑板",
            cal:"292",
            color:"blue"
          },
          {
            title:"滑冰，滑雪",
            cal:"437",
            color:"pink"
          },
          {
            title:"击剑",
            cal:"364",
            color:"lightgray"
          }
        ]
      }
    },
    methods:{
      inputchange(e){
          this.sportcal=e.mp.detail.value;
        },
      detail(item,index){
        // wx.showModal({
        //   title:"提示",
        //   content:"是否将此项运动加入今日项目中",
        //   success:res=>{
        //     if(res.confirm){
        //
        //       wx.navigateTo({
        //         url:"../Daily_intake/main"
        //       })
        //     }
        //   }
        // })
        this.hiddenmodalsport=true;
        this.sportitem=item;
      },
      cancelM(){
        this.hiddenmodalsport=false;
      },
      confirmM(){
        this.hiddenmodalsport=false;

        this.globalData.allcal+=parseInt(this.sportcal)*parseInt(this.sportitem.cal);
        this.globalData.scal=parseInt(this.sportcal)*parseInt(this.sportitem.cal);
        this.sportlist.push(this.sportitem);
        this.globalData.sport= this.sportlist;
        wx.navigateTo({
          url:"../Daily_intake/main"
        })
      }
    }
  }
</script>
<style scoped>

</style>
