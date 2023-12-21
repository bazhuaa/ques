<template>
  <div class="hello">
    <h1>计算任务</h1>
    <p>
      指导语：<br />
      请从2024依次减去17，并大声说出你的计算结果，<br />
      例如2007、1990……<br />
      如果计算错误，将需要停止，并从头开始计算
    </p>

    <button class="btn btn-info" @click="startTime" v-if="!start">
      开始倒计时
    </button>
    <button class="btn btn-success" v-else style="margin-right: 10px">
      倒计时{{ time }}s
    </button>
    <!-- <button class="btn btn-info" v-if="start" @click="restart">重新开始</button> -->
    <audio src="compute.mp3" autoplay></audio>
  </div>
</template>

<script>
export default {
  name: "quesTable",
  props: {},
  data() {
    this.timer = null;
    return {
      time: 180, //todo180
      start: false,
    };
  },
  methods: {
    restart() {
      clearInterval(this.timer);
      this.timer = null;
      this.time = 180;
      this.start = false;
    },
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
