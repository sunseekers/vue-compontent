<template>
  <!--前端列表搜索 用css 属性选择器与搜索过滤实例页面-->
  <div class="search-wrapper">
    <div class="search">
      <input v-model="searchWord" type="text" placeholder="搜索" />
      <span class="iconfont searcIcon">&#xe62b;</span>
    </div>
    <div class="content">
      <div class="select-all" @click="selectAll">
        <span>全选</span>
        <span v-html="allSelectIcon" class="iconfont empty-icon"></span>
      </div>
      <div class="data-list">
        <div class="grade" @click="selectCity(item)" v-for="(item, index) in showList" :key="index"  :data-search="item.city">
            <div class="select-all">
              <span class="grade-name">{{ item.cityName }}</span>
              <span v-html="classSelectIcon(item)" class="iconfont empty-icon"></span>
            </div>
          </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  props: {
    showList: {
      type: Array,
      default: () => {
        return [
          {
            city: '重庆市chongqing',
            cityName: '重庆市'
          },
          {
            city: '哈尔滨市haerbing',
            cityName: '哈尔滨市'
          },
          {
            city: '长春市changchun',
            cityName: '长春市'
          },
          {
            city: '长沙changsha',
            cityName: '长沙',
          },
          {
            city: '上海shanghai',
            cityName: '上海'
          },
          {
            city: '北京biejing',
            cityName: '北京',
          },
        ]
      }
    }
  },
  data() {
    return {
      searchWord: '',
      selectedList: [],
      showSearchList: [],
      eleStyle:"",
      dropedGrade: [] // 那些班级展开了
    }
  },
  computed: {
    allSelectIcon() {
      const bol =
        this.selectedList.length &&
        this.selectedList.length === this.showList.length

      return bol ? '&#xe6b2;' : '&#xe6b3;'
    }
  },
  created() {
    this.eleStyle = document.createElement("style")
    document.head.appendChild(this.eleStyle)
  },
  watch: {
    searchWord(nv) {
          this.eleStyle.innerHTML = nv ? `[data-search]:not([data-search*="${nv}"]) { display: none; }` : '';
    }
  },
  methods: {
    // 选择所有
    selectAll() {
      const bol = this.selectedList.length === this.showList.length
      bol
        ? (this.selectedList = [])
        : (this.selectedList = JSON.parse(JSON.stringify(this.showList)))
    },
    selectCity(item) {
      const index = this.selectedList.findIndex(ele=>item.cityName===ele.cityName)
      index === -1 ?this.selectedList.push(item):this.selectedList.splice(index,1)
    },
    classSelectIcon(item) {
      const bol = this.selectedList.findIndex(
        ele => ele.cityName === item.cityName
      )
      return bol > -1 ? '&#xe6b2;' : '&#xe6b3;'
    },


  }
}
</script>

<style scoped lang="scss">
.search-wrapper {
  p {
    text-align: center;
  }
  .content {
    width: 100%;
    height: 100%;
    overflow-y: scroll;
    padding: 56px 0 60px 0;
    .select-all {
      width: 100%;
      height: 52px;
      position: relative;
      padding: 0 15px 0 38px;
      background: #fff;
      display: flex;
      justify-content: space-between;
      align-items: center;
      font-size: 16px;
      font-family: PingFangSC-Regular, PingFangSC;
      font-weight: 400;
      color: rgba(144, 144, 144, 1);
      border-bottom: 1px solid #f3f3f3;
      overflow: hidden;
      .is-evaluated {
        width: 46px;
        background: rgba(254, 181, 76, 0.15);
        border-radius: 9px;
        height: 16px;
        font-size: 11px;
        font-family: PingFangSC-Regular, PingFang SC;
        font-weight: 400;
        color: rgba(254, 181, 76, 1);
        line-height: 18px;
        margin-left: 10px;
        text-align: center;
        display: inline-block;
      }
      .empty-icon {
        color: #37ca7c;
      }
      .name {
        width: 100%;
        height: 52px;
        background: #fff;
        display: flex;
        justify-content: space-between;
        align-items: center;
      }
    }
    .data-list {
      width: 100%;
      padding-bottom: 60px;
      overflow-y: scroll;
      -webkit-overflow-scrolling: touch;

      .grade {
        color: #000;
      }
      .grade-name {
        color: #000;
      }
    }
    .drop-icon {
      position: absolute;
      left: 10px;
      top: 50%;
      transform: translateY(-50%);
    }
  }
}
</style>
