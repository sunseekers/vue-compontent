<template>
  <div class="list">
    <div
      class="item "
      v-for="(item, index) in list"
      :key="`list${index}`"
      @click="detail(item, index)"
      :class="{ 'red-list': item.msgState === 1 }"
    >
      <div>
        <span>申请时间:</span>
        <span class="time">{{ item.applicationTime }}</span>
      </div>
      <div>
        <span>补卡时间:</span>
        <span class="time">{{ item.time }}</span>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  props: {
    list: {
      type: Array,
      default: () => {
        return [
          {
            applicationTime: '899',
            time: '898'
          },
          {
            applicationTime: '899',
            time: '898'
          },
          {
            applicationTime: '899',
            time: '898'
          }
        ]
      }
    }
  },

  methods: {
    detail(item, index) {
      this.$emit('goToDetail', { item, index })
    }
  }
}
</script>

<style scoped lang="scss">
.list {
  .item {
    border: 1px red solid;
    display: flex;
    justify-content: center;
    flex-direction: column;
    padding: 0 15px;
    height: 100px;
    background: rgba(255, 255, 255, 1);
    margin-top: 10px;
    border-radius: 4px;
    font-size: 14px;
    font-family: PingFangSC-Regular, PingFang SC;
    font-weight: 400;
    color: rgba(144, 144, 144, 1);

    .time {
      padding-left: 10px;
      color: rgba(38, 38, 38, 1);
    }
    div {
      text-align: left;
      padding-top: 10px;
    }
  }
}
</style>
