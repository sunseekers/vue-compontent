<template>
  <div class="wrapper">
    <form>
      <fieldset>
        <legend>问卷调查</legend>
        <ol class="cs-ques-ul">
          <li class="cs-ques-li">
            <input type="radio" name="ques1" required>1-3年
            <input type="radio" name="ques1">3-5年
            <input type="radio" name="ques1">5年以上
            <h4 class="cs-caption">你从事前端几年了？</h4>
          </li>
          <li class="cs-ques-li">
            <input type="radio" name="ques2" required>1-3小时
            <input type="radio" name="ques2">3-5小时
            <input type="radio" name="ques2">小时以上
            <h4 class="cs-caption">你每周多少业余时间用来学习前端技术？</h4>
          </li>
          <li class="cs-ques-li">
            <input type="radio" name="ques3" required>1-3本
            <input type="radio" name="ques3">3-5本
            <input type="radio" name="ques3">5本以上
            <h4 class="cs-caption">你每年买多少本前端相关数据？</h4>
          </li>
          <li class="cs-ques-li">
            <textarea></textarea>
            <h4 class="cs-caption">有什么其它想说的？</h4>
          </li>
        </ol>
        <p><input type="submit" value="提交"></p>
      </fieldset>
    </form>
  </div>
</template>

<script>
export default {
	data() {
		return {
		}
	},
}
</script>

<style scoped lang="scss">
.cs-ques-ul {
  counter-reset: quesIndex;
}
.cs-ques-li {
  display: table;
  width: 100%;
  position: relative;
}
/* 前面序号计数显示与定位 */
.cs-ques-li::before {
  counter-increment: quesIndex;
  content: counter(quesIndex) ".";
  position: absolute;
  top: 0;
  margin: 0 0 0 -10px;
}
.cs-caption {
  display: table-caption;
  caption-side: top;
}
/* 标记必选还是可选 */
:optional ~ .cs-caption::after {
  content: "（可选）";
  color: gray;
}
:required ~ .cs-caption::after {
  content: "（必选）";
  color: red;
}
</style>
