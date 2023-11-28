<template>
  <div class="hello">
    <h1>静坐时间</h1>
    <p>
      指导语：<br />
      请您静坐5分钟，测量基础生理状态。<br />
      请按下holter中间的按钮，并点击下方按钮开始倒计时!
    </p>

    <button class="btn btn-info" @click="startTime" v-if="!start">开始倒计时</button>
    <button class="btn btn-success" v-else>倒计时{{ time }}s</button>
  </div>
</template>

<script>
export default {
  name: "quesTable",
  props: {},
  data() {
    this.timer = null;
    return {
      time: 300, //todo 300
      start: false,
    };
  },
  methods: {
    nextStep() {
      this.$emit("finish");
    },
    startTime() {
      this.start = true;
      this.timer = setInterval(() => {
        this.time--;
        if (this.time == 0) {
          this.nextStep();
          clearInterval(this.timer);
        }
      }, 1000);
    },
  },
  created() {},
};
</script>

<style scoped></style>
