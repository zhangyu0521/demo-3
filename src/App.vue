<template>
  <div class="app-container">
    <h1 ref="myh1">App 根组件</h1>
    <button @click="showThis">打印this</button>
    <button @click="onReset">重置Left组件的count值为0</button>
    <hr />
    <input type="text" v-if="inputVisible" @blur="showButton" ref="iptRef">
    <button v-else @click="showInput">展示按钮</button>

    <hr />
    <div class="box">
      <!-- 渲染 Left 组件和 Right 组件 -->
      <Left ref="comLeft"></Left>
    </div>
  </div>
</template>

<script>
import Left from '@/components/Left.vue';
export default {
  methods: {
    showThis() {
      // console.log(this.$refs.myh1);
      console.log(this)
      this.$refs.myh1.style.color = 'red';
    },
    showInput() {
      //1.切换布尔值，把文本框展示出来
      this.inputVisible = true;
      //2.让展示出来的文本框，自动获得焦点
      this.$nextTick(() => {
        this.$refs.iptRef.focus();
      })
    },
    showButton() {
      this.inputVisible = false;
    },
    //点击按钮，重置Left组件的count值
    onReset() {
      this.$refs.comLeft.resetCount();
    }
  },
  data() {
    return {
      //控制输入框和按钮的按需切换；
      //默认值为false，表示默认展示按钮，隐藏输入框
      inputVisible: false
    }
  },
  components: {
    Left
  }
}
</script>

<style lang="less">
.app-container {
  padding: 1px 20px 20px;
  background-color: #efefef;
}
.box {
  display: flex;
}
</style>
