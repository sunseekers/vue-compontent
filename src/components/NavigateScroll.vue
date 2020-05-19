<template>
  <div class="navigate-scroll">
    <div class='scroll-wrapper'
         ref="scroll">
      <div class="scroll-item"
           :ref="`item${index}`"
           @click="handleScroll(item,index)"
           v-for="(item,index) in list"
           :key='index'>{{item.label}}</div>
    </div>
  </div>
</template>
<style lang="scss" scoped>
.navigate-scroll {
  .scroll-wrapper {
    border: 1px red solid;
    overflow-x: auto;
    overflow-y: hidden;
    white-space: nowrap;
    transform: all ease 0.2s;
    -webkit-overflow-scrolling: touch;

    display: flex;
    align-items: center;
    .scroll-item {
      border: 1px red solid;
      height: 50px;
      padding: 15px;
    }
  }
}
</style>
<script>
import { setTimeout } from 'timers'
export default {
  data () {
    return {
      canScroll: true,
      list: [{
        label: '一年级'
      }, {
        label: '二年级'
      }, {
        label: '三年级'
      }, {
        label: '四年级'
      }, {
        label: '五年级'
      }, {
        label: '六年级'
      }, {
        label: '七年级'
      }, {
        label: '八年级'
      }, {
        label: '九年级'
      }, {
        label: '十年级'
      }, {
        label: '一1年级'
      }, {
        label: '一5年级'
      }, {
        label: '一3年级'
      }, {
        label: '一2年级'
      }]
    }
  },
  methods: {
    // 发生滚动
    handleScroll (item, index) {
      this.requestScrollAnimation(item, index)
    },
    // 滚动函数
    requestScrollAnimation (item, index) {
      if (!this.canScroll) return
      // 控制滚动，避免频繁的滚动
      this.canScroll = false
      const timer = setTimeout(() => {
        clearTimeout(timer)
        this.canScroll = true
      }, 300)
      // 计算需要滚动的距离
      const el = this.$refs[`item${index}`][0]
      const scrollWrapper = this.$refs.scroll
      // 计算滚动布长
      const steps = 10
      const offsetLeftFix = el.offsetLeft
      const scrollDistance = el.offsetLeft - scrollWrapper.offsetLeft
      const step = parseInt(scrollDistance / steps)
      // scrollTo 只会滚动整数距离这个需要注意一下，可能需要多走一步或者少走一步
      const trueDistance = step * steps
      let fixStep = 0
      const errorDistance = trueDistance - scrollDistance

      if (errorDistance < 0) {
        fixStep = -1
      }

      if (errorDistance > 0) {
        fixStep = 1
      }
      fixStep *= step < 0 ? -1 : 1
      this.scrollAnimation(item, scrollWrapper, step, steps, offsetLeftFix, fixStep)
    },
    scrollAnimation (item, scrollWrapper, step, steps, offsetLeftFix, fixStep, progress = 0) {
      let currentStep = progress
      const scrollTo = scrollWrapper.scrollLeft + step
      const stepNum = steps + fixStep
      if (currentStep < stepNum) {
        currentStep++
        scrollWrapper.scrollLeft = scrollTo
        const timer = setTimeout(() => {
          this.scrollAnimation(item, scrollWrapper, step, steps, offsetLeftFix, fixStep, currentStep)
          clearTimeout(timer)
        }, 16)
      } else {
        // 滚动最后一步
        const timer = setTimeout(() => {
          scrollWrapper.scrollLeft = offsetLeftFix
          clearTimeout(timer)
        }, 16)
      }
    }

  }

}
</script>
