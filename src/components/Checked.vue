<template>
  <div class="wrapper">
    <div>:default 伪类的默认使用</div>
    <!-- <p><input type="radio" name="pay" id="pay0" value="0" /> <label for="pay0">支付宝</label></p>
    <p><input type="radio" name="pay" id="pay1" value="1" checked /> <label for="pay1">微信</label></p>
    <p><input type="radio" name="pay" id="pay2" value="2" /> <label for="pay2">银行卡</label></p> -->

    <h4>标签的选择</h4>
    请选择你感兴趣的话题：<br />
    <input type="checkbox" id="topic1" /><label for="topic1" class="cs-topic">科技</label> <input type="checkbox" id="topic2" /><label for="topic2" class="cs-topic">体育</label> <input type="checkbox" id="topic3" /><label for="topic3" class="cs-topic">军事</label>
    <input type="checkbox" id="topic4" /><label for="topic4" class="cs-topic">娱乐</label> <input type="checkbox" id="topic5" /><label for="topic5" class="cs-topic">动漫</label> <input type="checkbox" id="topic6" /><label for="topic6" class="cs-topic">音乐</label>
    <input type="checkbox" id="topic7" /><label for="topic7" class="cs-topic">电影</label> <input type="checkbox" id="topic8" /><label for="topic8" class="cs-topic">生活</label>
    <p>您已选择<span class="cs-topic-counter"></span>个话题。</p>

    <h4>图像的选择</h4>
    请选择壁纸：<br />
    <input type="radio" id="wallpaper1" name="wallpaper" checked />
    <label for="wallpaper1" class="cs-wallpaper">
      <img src="../assets/logo.png" class="cs-wallpaper-img" />
    </label>
    <input type="radio" id="wallpaper2" name="wallpaper" />
    <label for="wallpaper2" class="cs-wallpaper">
      <img src="../assets/logo.png" class="cs-wallpaper-img" />
    </label>
    <input type="radio" id="wallpaper3" name="wallpaper" />
    <label for="wallpaper3" class="cs-wallpaper">
      <img src="../assets/logo.png" class="cs-wallpaper-img" />
    </label>
    <input type="radio" id="wallpaper4" name="wallpaper" />
    <label for="wallpaper4" class="cs-wallpaper">
      <img src="../assets/logo.png" class="cs-wallpaper-img" />
    </label>
    <input type="radio" id="wallpaper5" name="wallpaper" />
    <label for="wallpaper5" class="cs-wallpaper">
      <img src="../assets/logo.png" class="cs-wallpaper-img" />
    </label>
    <input type="radio" id="wallpaper6" name="wallpaper" />
    <label for="wallpaper6" class="cs-wallpaper">
      <img src="../assets/logo.png" class="cs-wallpaper-img" />
    </label>
  </div>
</template>

<script>
export default {}
</script>

<style scoped lang="scss">
p {
  text-align: left;
}
input:default + label::after {
  content: '（推荐）';
}
[type='checkbox'],
[type='radio'] {
  position: absolute;
  clip: rect(0 0 0 0);
}

.cs-topic {
  display: inline-block;
  width: 64px;
  margin-top: 5px;
  padding: 5px 0;
  border: 1px solid silver;
  text-align: center;
  cursor: pointer;
}
.cs-topic:hover {
  border-color: gray;
}
:checked + .cs-topic {
  border-color: deepskyblue;
  background-color: azure;
}
/* 选择计数器 */
body {
  counter-reset: topicCounter;
}
:checked + .cs-topic {
  counter-increment: topicCounter;
}
.cs-topic-counter::before {
  color: red;
  margin: 0 2px;
  content: counter(topicCounter);
}

.cs-wallpaper {
  display: inline-block;
  width: 90px;
  height: 120px;
  margin-top: 5px;
  vertical-align: bottom;
  position: relative;
  overflow: hidden;
  cursor: pointer;
}
.cs-wallpaper-img {
  display: block;
  height: 100%;
  width: 100%;
}
:checked + .cs-wallpaper::before {
  content: '';
  position: absolute;
  left: 0;
  right: 0;
  top: 0;
  bottom: 0;
  border: 2px solid deepskyblue;
  background: linear-gradient(-135deg, deepskyblue 14px, transparent 15px);
}
:checked + .cs-wallpaper::after {
  content: '';
  position: absolute;
  right: 2px;
  top: 3px;
  width: 8px;
  height: 3px;
  color: white;
  border-left: 2px solid;
  border-bottom: 2px solid;
  -ms-transform: rotate(-45deg);
  transform: rotate(-45deg);
}
</style>
