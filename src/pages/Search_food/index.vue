<template>
  <div id="wrap">
    <!--<input type="search">-->
    <ul class="list">
      <li @click="commonfood()">
        <text :class="{text:isfood}">常见食物</text>
        <span :class="{span2:isfood}"></span>
      </li>
      <li @click="customfood()">
        <text :class="{text:!isfood}">自定义食物</text>
        <span :class="{span2:!isfood}"></span>
      </li>
    </ul>
    <section v-show="isfood">
      <i-cell-group>
        <i-cell  @click="addfood(item,index)" v-for="(item,index) in list" :title="item.name" is-link>{{item.cal}}千卡/100克</i-cell>

      </i-cell-group>
    </section>
    <section v-show="!isfood">
      <i-modal title="基本信息" :visible="visible1" @ok="handleok()" @cancel="handleconcel()">
        <view class="box"><label for="">食物名称:</label><input @change="inputchange" type="text"  placeholder="如：水果沙拉"/></view>
        <view class="box"><label for="">单位:</label><input type="text" value="100克" disabled="disabled"></view>
        <view class="box"><label for="">热量:</label><input @change="inputchange1" type="text"  placeholder="如100"></view>
      </i-modal>
      <i-cell-group>
        <i-cell @click="addcustomfood(item,index)" v-for="(item,index) in listcustom" :title="item.name" is-link>{{item.cal}}千卡/100克</i-cell>
        <button class="btn" @click="handleOpen1()">+添加自定义食物</button>
      </i-cell-group>
    </section>
    <modal v-if="hiddenmodalput" title="请填写克数" confirm-text="确定" cancel-text="取消" @cancel="cancelM" @confirm="confirmM">
        <input type="text" @change="inputchange2" style="border: 1px solid lightgray;">
    </modal>
  </div>
</template>
<script>
  export default {
    data(){
      return{
        // cal:"",
        cancal:"",
        // itemnew:{},
        // indexnew:"",
        hiddenmodalput:false,
        isfood:true,
        visible1:false,
        listcustom:[],
        listextmorning:[],
        listextnoon:[],
        listextnight:[],
        foodname:"",
        foodcal:"",
        btnshow:true,
        timekey:"",
        list:[
          {image:"",name:"米饭",cal:"116"},
          {image:"",name:"杂米饭",cal:"125"},
          {image:"",name:"玉米饭",cal:"94"},
          {image:"",name:"五色五谷饭",cal:"128"},
          {image:"",name:"糯米饭",cal:"118"},
          {image:"",name:"红枣糯米饭",cal:"153"},
          {image:"",name:"田园菠萝炒米饭",cal:"173"},
          {image:"",name:"炒饭",cal:"188"},
          {image:"",name:"面包",cal:"313"},
          {image:"",name:"牛角面包",cal:"378"},
          {image:"",name:"葡萄干面包",cal:"260"},
          {image:"",name:"果料面包",cal:"279"},
          {image:"",name:"椰圈面包",cal:"320"},
          {image:"",name:"面条",cal:"301"},
          {image:"",name:"西红柿鸡蛋面",cal:"72"},
          {image:"",name:"荞麦面",cal:"391"},
          {image:"",name:"吐司面包",cal:"278"},
          {image:"",name:"全麦面包",cal:"246"},
          {image:"",name:"wonder面包片",cal:"246"},
          {image:"",name:"TIP面包片",cal:"254"},
          {image:"",name:"Harry面包片",cal:"247"},
          {image:"",name:"豆浆",cal:"31"},
          {image:"",name:"自制花生豆浆",cal:"47"},
          {image:"",name:"豆浆粉",cal:"426"},
          {image:"",name:"自制三色豆浆",cal:"29"},
          {image:"",name:"牛奶",cal:"54"},
          {image:"",name:"蒙牛高钙牛奶",cal:"59"},
          {image:"",name:"水果沙拉",cal:"136"},
          {image:"",name:"黑咖啡",cal:"1"},
          {image:"",name:"拿铁",cal:"44"},
          {image:"",name:"苹果",cal:"53"},
          {image:"",name:"香蕉",cal:"93"},
          {image:'',name:"梨",cal:"51"},
          {image:"",name:"葡萄",cal:"45"},
          {image:"",name:"橘子",cal:"44"},
          {image:"",name:"蓝莓",cal:"57"},
          {image:"",name:"柿子",cal:"74"},
          {image:"",name:"芒果",cal:"35"},
          {image:"",name:"提子",cal:""},
          {image:'',name:"草莓",cal:"32"},
          {image:"",name:"奇异果",cal:"61"},
          {image:"",name:"西瓜",cal:""},
          {image:"",name:"樱桃",cal:""},
          {image:"",name:"木瓜",cal:""},
          {image:"",name:"香瓜",cal:""},
          {image:"",name:"杨梅",cal:""},
          {image:"",name:"杨桃",cal:""},
          {image:"",name:"桃子",cal:""},
          {image:"",name:"火龙果",cal:""},
        ]
      }
    },
    methods:{
      customfood(){
        this.isfood=false;

      },
      commonfood(){
        this.isfood=true;
      },
      handleOpen1(){
        this.visible1=true;
      },
      handleok(){
        if(this.foodname && this.foodcal){
          this.btnshow=false;
          this.visible1=false;
          this.listcustom.push({name:this.foodname,cal:this.foodcal});
          console.log("啊啊啊"+JSON.stringify(this.listcustom));
        }else{
          wx.showModal({
            title:"提示",
            content:"请填写完整信息"
          })
        }

      },
      handleconcel(){
        this.btnshow=true;
        this.visible1=false;
      },
      inputchange(e){
        console.log("444"+JSON.stringify(e));
        this.foodname=e.mp.detail.value;
      },
      inputchange1(e){
        this.foodcal=e.mp.detail.value;
      },
      addfood(item,index){
        this.hiddenmodalput=true;
        // this.cal=item.cal;
        this.itemnew=item;
        this.indexnew=index;
        // wx.showModal({
        //   title:"提示",
        //   content:"确定将改食材加入今日饮食中,输入克数",
        //   success:res=>{
        //     if(res.confirm){
        //       console.log("caonima"+item.cal);
        //
        //
        //
        //     }
        //   }
        // })
      },
      addcustomfood(item,index){
        this.hiddenmodalput=true;
        // this.cal=item.cal;
        this.itemnew=item;
        this.indexnew=index;
      },
      inputchange2(e){
       this.cancal= e.mp.detail.value;

      },
      cancelM(){
        this.hiddenmodalput=false;
      },
      confirmM(){
        this.hiddenmodalput=false;
        this.globalData.vcal=(parseInt(this.cancal)/100)*parseInt(this.itemnew.cal);
        this.globalData.allcal+=(parseInt(this.cancal)/100)*parseInt(this.itemnew.cal);

        console.log("mlgj"+this.globalData.allcal);
        if(this.timekey=='morning'){
          this.listextmorning.push(this.itemnew);
          this.globalData.listmorning=this.listextmorning;
         // this.globalData.listmorning[ this.globalData.listmorning.length-1].cal=(parseInt(this.cancal)/100)*parseInt(this.itemnew.cal);
        }else if(this.timekey=='noon'){
          this.listextnoon.push(this.itemnew);
          this.globalData.listnoon= this.listextnoon;
        }else if(this.timekey=='night'){
          this.listextnight.push(this.itemnew);
          this.globalData.listafternoon=this.listextnight;
        }
        wx.navigateTo({
          url:"../Daily_intake/main"
        })

      }
    },
    created(){
      console.log("11111")
    },
    onLoad(options){

      console.log("uuuu"+JSON.stringify(options));
      let key=options.key;
      switch (key) {
        case 'morning':
          this.timekey='morning';
          break;
        case 'noon':
          this.timekey='noon';
          break;
        case 'night':
          this.timekey='night';
          break;
      }
    },
    onShow(){
      console.log("闹心"+JSON.stringify(this.list));

    }
  }
</script>
<style scoped>
  .list{
    width:100%;
    display: flex;
    height: 40px;
    border-bottom: 1px solid lightgray;
  }
.list li{
  width: 50%;
  text-align: center;
  height: 40px;
  /*line-height: 40px;*/
  display: flex;
  flex-direction: column;
}
  .list li text{
    color: gray;
    font-size: 14px;
    height: 39px;
  }
  .list li .text{
    color: orange;
    font-size: 14px;
    height: 39px;
  }
  .list li span{
    width: 100%;
    height: 1px;
    display: block;
    margin: 0 auto;
    background: lightgray;
  }
  .list li .span2{
    background: orange;
  }
  .btn{
    width: 80%;
    height: 40px;
    line-height: 40px;
    text-combine: center;
    border: 1px solid orange;
    color: gray;
    font-size: 14px;
    background: white;
    margin-top: 80px;
  }
  .box{
    /*diplay:flex;*/
  }
  input{
    width: 80%;
    border: 1px solid lightgray;
    margin: 0 auto;

  }
</style>
