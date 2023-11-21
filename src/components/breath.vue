<template>
  <div class="hello">
    <h1>正念呼吸</h1>
    <p>
      指导语： <br />下面请跟随音频 调节你的呼吸和身体状态。<br />
      请花点时间，感觉一下。
    </p>
    <div>
      <audio style="margin: 10px auto" controls height="100" width="100">
        <source src="breath.mp3" type="audio/mpeg" />
        <embed height="50" width="100" src="breath.mp3" />
      </audio>
    </div>
    <button @click="nextStep" class="btn btn-success">下一步</button>
  </div>
</template>
margin: 0 auto;

<script>
export default {
  name: "quesTable",
  props: {},
  data() {
    return {};
  },
  methods: {
    nextStep() {
      this.$emit("finish");
    },
  },
  created() {},
};
</script>

<style scoped></style>
