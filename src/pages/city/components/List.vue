<template>
  <div class="list" ref="wrapper">
    <div>
      <div class="area">
        <div class="title border-topbottom">当前城市</div>
        <div class="button-list">
          <div class="button-wrapper">
            <div class="button">北京</div>
          </div>
        </div>
      </div>

      <div class="area">
        <div class="title border-topbottom">热门城市</div>
        <div class="button-list">
          <div
            class="button-wrapper"
            v-for="item of hotCities"
            :key="item.id"
          >
            <div class="button">{{item.name}}</div>
          </div>
        </div>
      </div>

      <div class="area"
           v-for="(item,key) of cities"
           :key="key"
           :ref="key"
      >
        <div class="title border-topbottom" >{{ key }}</div>
        <div class="item-list">
          <div class="item border-bottom"
               v-for="innerItem of item"
               :key="innerItem.id"
          >
            {{ innerItem.name }}
          </div>
        </div>
      </div>

    </div>
  </div>
</template>

<script>
import BScroll from 'better-scroll'
export default {
  name: 'CityList',
  props: {
    hotCities: Array,
    cities: Object,
    letter: String
  },
  mounted () {
    // 解决better-scroll无法使用问题
    // 原因：better-scroll加载快于数据加载，导致无法获取到数据长度
    // 解决办法：延长better-scroll加载时间
    this.scroll = new BScroll(this.$refs.wrapper)
    // setTimeout(() => {
    //   this.$nextTick(() => {
    //     this.scroll = new BScroll(this.$refs.wrapper, {
    //       click: true
    //     })
    //     // console.log(this.scroll)
    //   })
    // }, 400)
  },
  updated () {
    this.scroll.refresh()
  },
  watch: {
    letter () {
      console.log(this.letter)
      if (this.letter) {
        const element = this.$refs[this.letter][0]
        // console.log(element)
        this.scroll.scrollToElement(element)
      }
    }

  }

}
</script>

<style lang="stylus" scoped>
@import "~styles/varibles.styl"
.list{
  overflow hidden;
  position absolute;
  top 1.58rem;
  left 0;
  right 0;
  bottom 0;
}
.title{
  line-height .54rem;
  background #eee;
  padding-left .2rem;
  color #666;
  font-size .26rem;
}
.border-topbottom{
  &:before{
    border-color #ccc;
  }
  &:after{
    border-color #ccc;
  }
}
.border-bottom{
  &:before{
    border-color #ccc;
  }
}
.button-list{
  overflow hidden;
  padding .1rem .6rem .1rem .1rem;
}
.button-wrapper{
  float left;
  width 33.33%;
}
.button{
  padding .1rem 0;
  margin .1rem;
  text-align center;
  border .02rem solid #ccc;
  border-radius .06rem;

}
.item{
  line-height .76rem;
  padding-left .2rem;
}
</style>
