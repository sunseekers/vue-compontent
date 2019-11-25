<template>
  <!--移动端滚动分页-->
  <div class="scroll" @scroll="onScroll($event)">
    <List :list="list" @goToDetail="goToDetail" />
    <p class="list-loading-status">{{ getLoadingState() }}</p>
  </div>
</template>

<script>
export default {
  data() {
    return {
      list: [
        {
          applicationTime: '899',
          time: 'w'
        },
        {
          applicationTime: '899',
          time: '89w8'
        },
        {
          applicationTime: '899',
          time: '8w98'
        },
        {
          applicationTime: '899',
          time: '89w8'
        },
        {
          applicationTime: '899',
          time: '8w98'
        }
      ],
      param: {
        state: 0,
        page: 1,
        pageSize: 10
      },
      total: 0,
      hasMore: true
    }
  },
  components: {
    List: () => import('@/components/List.vue')
  },
  created() {
    this.getList()
  },
  methods: {
    // 获取数据
    getList() {
      if (this.param.page === 1) {
        this.total = 30
        this.param.page++

        // this.$api.Record.applyList(this.param).then(res => {
        //   console.log('接口返回数据', res)
        //   // 模拟数据
        //   if (res.code !== 0) return
        //   let data = res.data
        //   this.total = data.total
        //   this.param.page++
        //   this.list = data.list
        // })
      } else {
        // 根据请求到的数据去判断数据是否请求完了
        this.hasMore = this.list.length < this.total
        if (this.hasMore) {
          const newList = [
            {
              applicationTime: '89239',
              time: 'w2'
            },
            {
              applicationTime: '8929',
              time: '89w832'
            },
            {
              applicationTime: '8939',
              time: '这么8w98232'
            }
          ]
          this.list = [...this.list, ...newList]
          //   this.param.page++
          // this.$api.Record.applyList(this.param).then(res => {
          //   console.log('接口返回数据', res)

          //   if (res.code !== 0) return
          //   let data = res.data
          //   let newList = data.list
          //   this.list = [...this.list, ...newList]
          //   this.param.page++
          // console.log(this.list, '已经加载数据')
          // })
        }
      }
    },
    goToDetail() {},
    // 滚动加载数据
    onScroll(event) {
      this.onScrollData(event, this.getList)
    },
    onScrollData(event, callback) {
      const target = event.target
      // 滚动条的总高度
      const scrollHeight = target.scrollHeight
      // 可视区的高度
      const clientHeight = target.clientHeight
      // 距离顶部的距离
      const scrollTop = target.scrollTop
      // 滚动到底部,在安卓机低下有可能有小数，需要取整
      if (Math.ceil(scrollTop + clientHeight) >= scrollHeight) {
        callback()
      }
    },
    getLoadingState() {
      if (this.list && this.list.length > 0) {
        return '没有更多啦~'
      } else {
        return ''
      }
    }
  }
}
</script>

<style scoped lang="scss">
.scroll {
  overflow-y: scroll;
  height: 400px;
  -webkit-overflow-scrolling: touch;
  // border: 1px red solid;
  .list-loading-status {
    text-align: center;
    color: #d9d9d9;
    font-size: 12px;
    margin-top: 20px;
    margin-bottom: 20px;
  }
}
</style>
