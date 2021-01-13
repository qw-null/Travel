<template>
  <div>
    <div class="banner">
      <img class="banner-img"
           src="https://img1.qunarzz.com/travel/d8/1504/17/065682796320de.jpg_r_640x426x70_7b71e8a1.jpg"
           @click="handleBannerClick"
      >
      <div class="banner-info">
        <div class="banner-title">天安门广场</div>
        <div class="banner-number">
          <span class="iconfont banner-icon">&#xe7b3;</span>
          14
        </div>
      </div>
    </div>
    <common-gallary
      :imgs="imgs"
      v-show="showGallary"
      @close="handleGallaryClose"
    >
    </common-gallary>
  </div>
</template>

<script>
import CommonGallary from 'common/gallary/Gallary'
export default {
  name: 'DetailBanner',
  components: {
    CommonGallary
  },
  data () {
    return {
      showGallary: false,
      imgs: ['https://img1.qunarzz.com/vs_ceph_b2c_001/6ea9cf9b-6793-4fc9-be4c-9cfa27fefdd9.jpg_r_1280x840x95_0a95532e.jpg',
        'https://img1.qunarzz.com/vs_ceph_b2c_001/08d7d5bb-03e1-48a7-93fa-c4e764fd4156.jpg_r_1280x840x95_e0f4db70.jpg']
    }
  },
  methods: {
    handleBannerClick () {
      this.showGallary = true
    },
    handleGallaryClose () {
      this.showGallary = false
    }
  }

}
</script>

<style lang="stylus" scoped>
.banner{
  position relative;
  overflow hidden;
  height 0;
  padding-bottom 55%;
}
.banner-img{
  width 100%;
}
.banner-info{
  display flex;
  position absolute;
  left 0;
  right 0;
  bottom 0;
  line-height .6rem;
  color #fff;
  // 背景渐变
  background-image linear-gradient(top,rgba(0,0,0,0),rgba(0,0,0,0.8))
}
.banner-title{
  font-size .32rem;
  padding 0 .2rem;
  flex 1;
}
.banner-number{
  margin-top .14rem;
  padding 0 .3rem;
  line-height .4rem;
  height .32rem;
  border-radius .2rem;
  background rgba(0,0,0,.8);
  font-size .24rem;
}
.banner-icon{
  font-size .24rem;
}
</style>
