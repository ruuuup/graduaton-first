<template>
  <div class="content">
    <swiper :indicator-dots="indicatorDots" :autoplay="autoplay" :interval="interval" :duration="duration">
      <block v-for="item in imgUrls" >
        <swiper-item>
          <image :src="item" class="slide-image" width="355" height="100" />
        </swiper-item>
      </block>
    </swiper>
    <div class="section_top">
      <span class="span1"></span>
      <p class="text">瘦健康</p>
      <span class="span1"></span>
    </div>
    <div class="section_content">
        <div class="box">
          <dl>
            <dt>
              <i class="icon iconfont icon-caidan"></i>
            </dt>
            <dd>
              <h6>推荐菜单</h6>
            </dd>
          </dl>
          <dl>
            <dt>
              <i class="icon iconfont icon-yingyangpinggu"></i>
            </dt>
            <dd>
              <h6>每日摄入</h6>
            </dd>
          </dl>
          <dl>
            <dt>
              <i class="icon iconfont icon-tizhong"></i>
            </dt>
            <dd>
              <h6>体重记录</h6>
            </dd>
          </dl>
        </div>
        <div class="box">
        <dl>
          <dt>
            <i class="icon iconfont icon-jiankang"></i>
          </dt>
          <dd>
            <h6>健康体检</h6>
          </dd>
        </dl>
        <dl>
          <dt>
            <i class="icon iconfont icon-jianshen"></i>
          </dt>
          <dd>
            <h6>每日运动</h6>
          </dd>
        </dl>
        <dl>
          <dt>
            <i class="icon iconfont icon-lishi"></i>
          </dt>
          <dd>
            <h6>历史摄入</h6>
          </dd>
        </dl>
      </div>
    </div>
  </div>
</template>
<script>
  export default {
    data(){
      return{
        imgUrls: [
          'https://assets.imgix.net/sandbox/sandboxlogo.ai?page=2&fit=clamp&fm=png&w=640',
          'https://images.unsplash.com/photo-1551214012-84f95e060dee?w=640',
          'https://images.unsplash.com/photo-1551446591-142875a901a1?w=640'
        ],
        indicatorDots: false,
        autoplay: false,
        interval: 5000,
        duration: 1000
      }
    }
  }
</script>
<style scoped>
  .content{
    width: 100%;
    height: auto;
  }
  .section_top{
    width: 100%;
    height: 40px;
    margin-top: 10px;
    /*text-align: center;*/
    display: flex;
    justify-content: space-around;


  }
  .section_top .span1{
    width: 100px;
    height: 1px;
    background-color: gray;
    /*border: 1px solid gray;*/
    display: block;
    margin-top: 10px;
  }
  .section_top .text{
    font-size: 16px;
    color: gray;
  }
  .section_content{
    width: 100%;
    height: auto;
    display: flex;
    flex-direction: column;
  }
  .section_content .box{
    width: 95%;
    margin: 0 auto;
    height: 100px;
    display: flex;
  }
  .section_content .box dl{
    width: 31%;
    height: 100px;
  }
  .section_content .box dl dt{
    width: 100%;
    text-align: center;
    height: 60px;
    line-height: 60px;
  }
  .section_content .box dl dt .iconfont{
    font-size: 40px;
  }
  .section_content .box dl dt .icon-caidan{
    color: #38B591;

  }
  .section_content .box dl dt .icon-yingyangpinggu{
    color: #F65224;

  }
  .section_content .box dl dt .icon-tizhong{
    color: #FAB92F;

  }
  .section_content .box dl dt .icon-jiankang{
    color:#E15A8B;
  }
  .section_content .box dl dt .icon-jianshen{
    color: #468CC7;
  }
  .section_content .box dl dt .icon-lishi{
    color: #9C4236;
  }
  .section_content .box dl dd{
    width: 100%;
    text-align: center;
    height: 40px;
    line-height: 40px;
  }
  .section_content .box dl dd h6{
    font-size: 14px;
    color: gray;
  }
</style>
