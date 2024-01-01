<template>
  <div class="hello">
    <h1 style="font-size: 60px">请静坐，等待主试进来安排任务</h1>
    <audio src="task.MP3" autoplay></audio>
  </div>
</template>

<script>
export default {
  name: "quesTable",
  props: {},
  data() {
    this.timer = null;
    return {
      time: 600, //todo600
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
  created() {
    this.startTime();
  },
};
</script>

<style scoped></style>
