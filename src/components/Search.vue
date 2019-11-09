<template>
  <!--前端列表搜索-->
  <div class="search-wrapper">
    <div class="search">
      <input v-model="searchWord" type="text" placeholder="搜索" />
      <span class="iconfont searcIcon">&#xe62b;</span>
    </div>
    <div class="content">
      <div
        v-if="!searchWord && showList.length"
        class="select-all"
        @click="selectAll"
      >
        <span>全选</span>
        <span v-html="allSelectIcon" class="iconfont empty-icon"></span>
      </div>
      <div class="data-list" v-show="!searchWord && showList.length">
        <div
          class="grade"
          @click="dropGrade(grade)"
          v-for="(grade, index) in showList"
          :key="index"
        >
          <div class="select-all">
            <span
              class="iconfont drop-icon"
              v-html="
                dropedGrade.indexOf(grade.campusGradeId) > -1
                  ? '&#xe63f;'
                  : '&#xe6a1;'
              "
            ></span>
            <span class="grade-name">{{ grade.campusGradeName }}</span>
            <span
              @click.stop="selectGrade(grade)"
              v-html="gradeSelectIcon(grade)"
              class="iconfont empty-icon"
            ></span>
          </div>
          <div
            @click.stop="selectClass(classItem)"
            class="item"
            v-for="(classItem, index2) in grade.classList"
            :key="index2"
            v-show="dropedGrade.indexOf(grade.campusGradeId) > -1"
          >
            <div class="select-all">
              <span class="grade-name">{{ classItem.className }}</span>
              <span
                v-html="classSelectIcon(classItem)"
                class="iconfont empty-icon"
              ></span>
            </div>
          </div>
        </div>
      </div>
      <!-- 本地数据搜索出来的结果 -->
      <div class="data-list " v-show="searchWord && showSearchList.length">
        <div
          class="select-all "
          @click.stop="selectClass(item)"
          v-for="(item, index) in showSearchList"
          :key="index"
        >
          <div class="name">
            <span>{{ item.className }}</span>
            <span
              v-html="classSelectIcon(item)"
              class="iconfont empty-icon"
            ></span>
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
            campusGradeName: '一年级',
            campusGradeId: 1,
            classList: [
              {
                className: '一班',
                classId: 1,
                campusGradeId: 1
              },
              {
                className: '二班',
                classId: 2,
                campusGradeId: 1
              },
              {
                className: '三班',
                classId: 3,
                campusGradeId: 1
              },
              {
                className: '四班',
                classId: 4,
                campusGradeId: 1
              },
              {
                className: '五班',
                classId: 5,
                campusGradeId: 1
              }
            ]
          },
          {
            campusGradeName: '二年级',
            campusGradeId: 2,
            classList: [
              {
                className: '一班',
                classId: 6,
                campusGradeId: 2
              },
              {
                className: '二班',
                classId: 7,
                campusGradeId: 2
              },
              {
                className: '三班',
                classId: 8,
                campusGradeId: 2
              },
              {
                className: '四班',
                classId: 9,
                campusGradeId: 2
              },
              {
                className: '五班',
                classId: 10,
                campusGradeId: 2
              }
            ]
          }
        ]
      }
    }
  },
  data() {
    return {
      searchWord: '',
      selectedList: [],
      showSearchList: [],
      dropedGrade: [] // 那些班级展开了
    }
  },
  computed: {
    allSelectIcon() {
      const bol =
        this.selectedList.length &&
        this.selectedList.length === this.allClass.length

      return bol ? '&#xe6b2;' : '&#xe6b3;'
    }
  },
  created() {
    this.getAllClass()
  },
  watch: {
    searchWord(nv) {
      if (nv === '') {
        this.showSearchList = []

        return
      }
      // item.className.indexOf('') 返回所有的数据
      const filterList = this.allClass.filter(item =>
        item.className.includes(nv)
      )
      this.showSearchList = JSON.parse(JSON.stringify(filterList))
    }
  },
  methods: {
    getAllClass() {
      this.allClass = this.showList
        .map(item => {
          return item.classList
        })
        .flat()
    },
    // 选择所有
    selectAll() {
      const bol = this.selectedList.length === this.allClass.length
      bol
        ? (this.selectedList = [])
        : (this.selectedList = JSON.parse(JSON.stringify(this.allClass)))
    },
    // 展开年级
    dropGrade(grade) {
      const index = this.dropedGrade.findIndex(
        item => item === grade.campusGradeId
      )

      index > -1
        ? this.dropedGrade.splice(index, 1)
        : this.dropedGrade.push(grade.campusGradeId)
    },
    gradeSelectIcon(grade) {
      const length = this.selectedList.filter(
        item => item.campusGradeId === grade.campusGradeId
      ).length
      return length > 0 ? '&#xe6b2;' : '&#xe6b3;'
    },
    classSelectIcon(classItem) {
      const bol = this.selectedList.findIndex(
        item => item.classId === classItem.classId
      )
      return bol > -1 ? '&#xe6b2;' : '&#xe6b3;'
    },
    // 选择班级
    selectClass(classItem) {
      const bol = this.selectedList.findIndex(
        item => item.classId === classItem.classId
      )
      bol > -1
        ? this.selectedList.splice(bol, 1)
        : this.selectedList.push(classItem)
    },
    // 选择年级
    selectGrade(grade) {
      let exist = grade.classList.some(item => {
        return (
          this.selectedList.findIndex(el => item.classId === el.classId) !== -1
        )
      })
      if (exist) {
        // 取消全选
        grade.classList.forEach(item => {
          let index = this.selectedList.findIndex(
            el => item.classId === el.classId
          )
          if (index > -1) {
            this.selectedList.splice(index, 1)
            console.log(index, 'index')
          }
        })
      } else {
        // 全选
        grade.classList.forEach(item => {
          this.selectedList.push(item)
        })
      }
    }
  }
}
</script>

<style scoped lang="scss">
.search-wrapper {
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
