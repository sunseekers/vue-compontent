<template>
  <!--移动端滚动分页-->
  <div class="scroll" id="scrollArea">
    <div class="list">
      <div class="item" v-for="(item, index) in list" :key="`list${index}`" @click="detail(item, index)" :class="{ 'red-list': item.msgState === 1 }">
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
    <p class="list-loading-status">{{ getLoadingState() }}</p>
  </div>
</template>

<script>
export default {
  data() {
    return {
      list: [
        
        {
          applicationTime: '1899',
          time: '89w8'
        },
        {
          applicationTime: '2899',
          time: '8w98'
        },
        {
          applicationTime: '3899',
          time: '89w8'
        },
        {
          applicationTime: '4899',
          time: '8w98'
        },        {
          applicationTime: '5899',
          time: 'w'
        },
        {
          applicationTime: '6899',
          time: '89w8'
        },      {
          applicationTime: '7899',
          time: 'w'
        },
        {
          applicationTime: 'qqqqq8899',
          time: '89w8'
        }
      ],
      param: {
        state: 0,
        page: 1,
        pageSize: 10
      },
      total: 0,
      hasMore: true,
      observer:""
    }
  },
  mounted() {
    this.getList()
    this.getObserver()
  },
  methods: {
    getObserver(){
     const observer = new IntersectionObserver(entry=>{
       if(entry[0]&&entry[0].isIntersecting){
         this.getList()
       }
     });
    observer.observe(document.querySelector('.list-loading-status'))
    },
    // 获取数据
    getList() {
      if (this.param.page === 1) {
        this.total = 20
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
				console.log(this.list.length);
        this.hasMore = this.list.length < this.total
        if (this.hasMore) {
          const newList = [
            {
              applicationTime: 'q989239',
              time: 'w2'
            },
            {
              applicationTime: '28929',
              time: '89w832'
            },
            {
              applicationTime: '8q939',
              time: '8w98232'
            },{
              applicationTime: 'q8929',
              time: '89w832'
            },
            {
              applicationTime: 'q8939',
              time: '8w98232'
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
  height: 100%;
  border: 1px red solid;
  -webkit-overflow-scrolling: touch;
  // border: 1px red solid;
  .list-loading-status {
    text-align: center;
    color: #d9d9d9;
    font-size: 12px;
    margin-top: 20px;
    margin-bottom: 20px;
  }
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
    &:empty + .empty::before {
      display: inline-block;
      padding-top: 40px;
      content: "暂无数据";
      color: #000;
    }
  }
}
</style>
