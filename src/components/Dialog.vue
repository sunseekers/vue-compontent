<template>
  <!--弹窗-->
  <div class="dialog-wrapper">
    <div class="dialog">
      <div class="title">评分</div>
      <div class="score">
        <span class="title">{{score.title}}</span>
        <span class="iconfont font"
              @click="switchScore">&#xe629;</span>
        <input placeholder="请输入分数"
               v-model='scoreVal'
               class="content"
               type='number' />
      </div>
      <div class='tip'>
        <span>可评价分数</span>
        <span>{{score.maxScore}}</span>
        <span>~</span>
        <span>{{score.minScore}}</span>
      </div>
      <div class="button">
        <button @click="cancel">取消</button>
        <button @click="confirm">确定</button>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  props: {
    score: {
      type: Object,
      default: () => {
        return {
          id: 1195,
          itemScore: 10,
          maxScore: 10,
          minScore: 10
        }
      }
    }
  },
  data () {
    return {
      scoreVal: ''
    }
  },
  methods: {
    cancel () {
      console.log('取消事件')
    },
    confirm () {
      console.log('确认事件')
    },
    switchScore () {
      console.log('切换分数')
    }
  }
}
</script>

<style scoped lang="scss">
.dialog-wrapper {
  width: 100%;
  height: 100%;
  position: fixed;
  top: 0;
  left: 0;
  background: rgba(0, 0, 0, 0.5);
  .dialog {
    width: 100%;
    position: fixed;
    top: 50%;
    left: 50%;
    transform: translate(-50%, -50%);
    background-color: #fff;
    width: 296px;
    height: 180px;
    background: rgba(255, 255, 255, 1);
    border-radius: 12px;
    display: flex;
    align-items: center;
    flex-direction: column;
    .title {
      font-size: 17px;
      font-weight: 400;
      color: rgba(38, 38, 38, 1);
      line-height: 60px;
    }
    .score {
      width: 250px;
      height: 40px;
      background: rgba(248, 248, 248, 1);
      font-size: 16px;
      font-weight: 400;
      color: rgba(179, 179, 179, 1);
      display: flex;
      align-items: center;
      .title {
        width: 56px;
        text-align: center;
        font-weight: 400;
        color: rgba(144, 144, 144, 1);
      }
    }
  }
}
</style>
