<template>
  <div class="load-wrapper">
    <div class="half">
      <img class="img"
           v-for="leftIndex in leftImgIndexes"
           :src="imgList[leftIndex]"
           :key="leftIndex" />
    </div>
    <div class="half">
      <img class="img"
           v-for="rightIndex in rightImgIndexes"
           :src="imgList[rightIndex]"
           :key="rightIndex" />
    </div>
  </div>
</template>
<script>
export default {
  data() {
    return {
      imgList: [require('../assets/2.jpeg'), require('../assets/5.jpeg'), require('../assets/6.jpeg'),
        require('../assets/3.jpeg'), require('../assets/4.jpeg'), require('../assets/2.jpeg'), require('../assets/8.jpeg'), require('../assets/7.jpeg') ],
      heights: [],
      leftImgIndexes: [],
      rightImgIndexes: [],
      rightHeights: [],
      leftHeights: [],
      halfInnerWidth: document.body.clientWidth
    }
  },
  mounted() {
    this.greedy()
  },
  methods: {
    // 获取图片的高度
    loadImgHeights(imgList) {
      return new Promise((resolve, reject) => {
        const length = imgList.length
        let count = 0
        const heights = []
        // 图片加载获取相关的信息
        const load = (index) => {
          let img = new Image()
          // 图片加载完了，把所有图片对应的高度存起来，结束这次循环
          const checkIfFinished = () => {
            count++
            if (count === length) {
              resolve(heights)
            }
          }
          // 图片加载的时候，获取图片的信息
          img.onload = () => {
            const ratio = img.height / img.width
            const halfHeight = ratio * this.halfInnerWidth
            heights[index] = halfHeight
            checkIfFinished()
          }
          // 图片加载失败
          img.onerror = () => {
            heights[index] = 0
            checkIfFinished()
          }
          // 图片的链接
          img.src = imgList[index]
        }
        imgList.forEach((img, index) => load(index))
      })
    },
    // 左右两边图片的数组
    greedy() {
      const sum = list => list.reduce((pre, next) => pre + next, 0)
      this.loadImgHeights(this.imgList).then(res => {
        res.forEach((height, index) => {
          if (sum(this.leftHeights) > sum(this.rightHeights)) {
            this.rightImgIndexes.push(index)
            this.rightHeights.push(height)
          } else {
            this.leftImgIndexes.push(index)
            this.leftHeights.push(height)
          }
        })
      })
    }

  }

}
</script>
<style scoped lang="scss">
.load-wrapper {
  display: flex;
}
.half {
  width: 50%;
  padding: 8px;
}
.img {
  margin-bottom: 10px;
}
</style>
