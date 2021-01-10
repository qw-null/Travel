<template>
  <div class="wrapper">
    <swiper :options="swiperOption">
      <!-- slides -->
      <swiper-slide v-for=" item of swiperList" :key="item.id">
        <img class="swiper-img" :src="item.imgUrl"/>
      </swiper-slide>
      <!-- Optional controls -->
      <div class="swiper-pagination"  slot="pagination"></div>
    </swiper>
  </div>

</template>

<script>
export default {
  name: 'HomeSwiper',
  data: function () {
    return {
      swiperOption: {
        pagination: '.swiper-pagination',
        loop: true
      },
      swiperList: [{
        id: '001',
        imgUrl: 'https://imgs.qunarzz.com/vs_ceph_vcimg/f03f5ac90ae59d0d9c6332a2bfd9782e.jpeg'
      }, {
        id: '002',
        imgUrl: 'https://imgs.qunarzz.com/vs_ceph_vcimg/f7813c9431796cc32ae7b7a78447342e.jpeg'
      }, {
        id: '003',
        imgUrl: 'https://gw.alicdn.com/imgextra/i3/O1CN01Et2D6j26f9bPBpW7p_!!6000000007688-2-tps-1125-352.png_790x10000.jpg'
      }]
    }
  }
}

</script>

<style lang="stylus" scoped>
.wrapper >>> .swiper-pagination-bullet-active{
  background: #fff
}
.wrapper{
  overflow:hidden
  width:100%
  height:0
  padding-bottom: 31.25%
  background: #eee
  .swiper-img{
    width: 100%
  }
}

</style>
