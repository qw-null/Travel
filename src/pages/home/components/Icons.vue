<template>
  <div class="icons">
    <swiper :options="swiperOption">
      <swiper-slide
        v-for="(page,key) of pages"
        :key="key">
        <div class="icon"
             v-for="item of page"
             :key="item.id">
          <div class="icon-img">
            <img class="icon-img-content" :src="item.imgUrl">
          </div>
          <p class="icon-desc">{{item.title}}</p>
        </div>
      </swiper-slide>

    </swiper>
  </div>

</template>

<script>
export default {
  name: 'HomeIcons',
  props: {
    iconList: Array
  },
  data: function () {
    return {
      swiperOption: {
        autoplay: false
      }
    }
  },
  computed: {
    pages () {
      const pages = []
      this.iconList.forEach((item, index) => {
        // 向下取整
        const page = Math.floor(index / 8)
        if (!pages[page]) {
          pages[page] = []
        }
        pages[page].push(item)
      })
      // console.log(pages)
      return pages
    }
  }

}
</script>

<style lang="stylus" scoped>
  @import "~styles/varibles.styl"
  @import "~styles/mixins.styl"
  .icons >>> .swiper-container{
    height: 0;
    padding-bottom: 50%;
  }
  .icons{
    margin-top: .2rem;
    .icon {
      position: relative;
      overflow: hidden;
      float: left;
      height: 0;
      width: 25%;
      padding-bottom: 25%;
      .icon-img {
        position: absolute;
        top: 0;
        left: 0;
        right: 0;
        bottom: .44rem;
        box-sizing: border-box;
        padding: .1rem;
        .icon-img-content{
          display: block;
          margin: 0 auto;
          height: 100%;
        }
      }
      .icon-desc {
        position: absolute;
        left: 0;
        right: 0;
        bottom: 0;
        height: .44rem;
        line-height: .44rem;
        text-align: center;
        color: $darkTextColor;
        ellipsis()
      }
    }

}

</style>
