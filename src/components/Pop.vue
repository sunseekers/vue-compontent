<template>
  <div class="wrapper">
    <div class='clicka'
         @click="wrapperShowhandld">8989</div>
    <div class="mask"
         @click="handleShow"
         v-show='dialogShow'
         :class="[`${isShow?'show':'hidden'}`]">
      <div class="pop">
        hhhhh
      </div>
    </div>
  </div>
</template>
<script>
export default {
  data() {
    return {
      isShow: false,
      dialogShow: false// 这个是外面来控制的
    }
  },
  watch: {
    isShow(val) {
      if (!val) {
        const timer = setTimeout(() => {
          clearTimeout(timer)
          this.dialogShow = false
        }, 300)
      }
    }
  },
  methods: {
    handleShow() {
      this.isShow = !this.isShow
    },
    wrapperShowhandld() {
      this.isShow = !this.isShow
      // 为了确保动画的正常执行
      const timer = setTimeout(() => {
        clearTimeout(timer)
        this.dialogShow = !this.dialogShow
      }, 300)
    }
  }

}
</script>
<style scoped lang="scss">
.clicka {
  height: 30px;
}
.mask {
  position: fixed;
  left: 0;
  top: 30px;
  right: 0;
  bottom: 0;
  background-color: rgba(0, 0, 0, 0.5);
  overflow: hidden;
}
.show {
  animation: showanimate 0.3s ease;
}
.hidden {
  animation: hiddenanimate 0.3s ease;
}
.pop {
  border: 1px red solid;
  background: #fff;
  margin-top: 40px;
  height: calc(100% - 40px);
  width: 100%;
}

@keyframes hiddenanimate {
  from {
    height: 100%;
    top: 30px;
  }
  to {
    height: 0;
    top: 100%;
  }
}
@keyframes showanimate {
  from {
    height: 0;
    top: 100%;
  }
  to {
    height: 100%;
    top: 30px;
  }
}
</style>
