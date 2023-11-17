<template>
  <div class="hello">
    <h1>实验结束，感谢您的参与！</h1>
    <p>请取下生理设备，填写被试单并领取被试费</p>
    <button @click="nextStep" class="btn btn-info">重新开始</button>
  </div>
</template>

<script>
export default {
  name: "quesTable",
  props: {},
  methods: {
    nextStep() {
      this.$emit("finish");
    },
  },
};
</script>

<style scoped></style>
