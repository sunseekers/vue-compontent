<template>
  <!-- tab 切换 -->
  <div class="tab">
    <div
      v-for="(item, index) in tab"
      :key="`tab${index}`"
      :class="{ currentColor: currentIndex === index }"
      @click="switchTab(item, index)"
    >
      {{ item.label }}
    </div>
  </div>
</template>

<script>
export default {
  props: {
    tab: {
      type: Array,
      default: () => {
        return [
          {
            label: '申请中',
            value: 0
          },
          {
            label: '通 过',
            value: 1
          },
          {
            label: '不通过',
            value: 2
          }
        ]
      }
    }
  },
  data() {
    return {
      currentIndex: 0
    }
  },
  methods: {
    switchTab(item, index) {
      this.currentIndex = index
      // 进行切换数据处理
      console.log('进行切换数据处理', { item, index })
      this.$emit('switchTab', { item, index })
      // this.currentPage = 1
      // this.param.page = 1
      // this.param.state = index
      // this.list = []
      // this.getList()
      // this.getReplenishmentRed()
    }
  }
}
</script>

<style scoped lang="scss">
.tab {
  background-color: #ffffff;
  line-height: 46px;
  font-size: 18px;
  font-weight: 500;
  color: rgba(51, 51, 51, 1);
  display: flex;
  justify-content: space-around;
  align-items: center;
  position: relative;
  .currentColor {
    color: rgba(55, 202, 124, 1);
    border-bottom: 3px solid;
  }
}
</style>
