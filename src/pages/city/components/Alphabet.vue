<template>
  <ul class="list">
    <li class="item"
        v-for="key of letters"
        :ref="key"
        :key="key"
        @click="handleLetterClick"
        @touchstart="handleTouchStart"
        @touchmove="handleTouchMove"
        @touchend="handleTouchEnd"
    >
      {{ key }}
    </li>
  </ul>
</template>

<script>
export default {
  name: 'CityAlphabet',
  props: {
    cities: Object
  },
  data () {
    return {
      touchStatus: false,
      startY: 0,
      timer: null
    }
  },
  // 列表优化
  updated () {
    // 获取A距离顶部的位置
    this.startY = this.$refs['A'][0].offsetTop
  },
  computed: {
    letters () {
      const letters = []
      for (let i in this.cities) {
        letters.push(i)
      }
      return letters
    }
  },
  methods: {
    handleLetterClick: function (e) {
      this.$emit('change', e.target.innerText)
      // console.log(e.target.innerText)
    },
    handleTouchStart: function () {
      this.touchStatus = true
    },
    handleTouchMove (e) {
      if (this.touchStatus) {
        if (this.timer) {
          clearTimeout(this.timer)
        }
        // 函数节流的方式提高性能
        this.timer = setTimeout(() => {
          // 获取当前触碰位置距离A的距离
          const touchY = e.touches[0].clientY - 79
          // console.log(touchY)
          const index = Math.floor((touchY - this.startY) / 20)
          // console.log(index)
          if (index >= 0 && index < this.letters.length) {
            this.$emit('change', this.letters[index])
          }
        }, 16)
      }
    },
    handleTouchEnd () {
      this.touchStatus = false
    }
  }

}
</script>

<style lang="stylus" scoped>
@import "~styles/varibles.styl"
.list{
  display flex;
  flex-direction column;
  justify-content center;
  position absolute;
  top 1.58rem;
  right 0;
  bottom 0;
  width .4rem;
}
.item{
  line-height .4rem;
  text-align center;
  color $bgColor;
}

</style>
