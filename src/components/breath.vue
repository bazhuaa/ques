<template>
  <div class="hello">
    <h1>正念呼吸</h1>
    <p>
      指导语： <br />下面请跟随音频 调节你的呼吸和身体状态。<br />
      请花点时间，感觉一下。
    </p>
    <audio src=""></audio>
    <button @click="nextStep" class="btn btn-success">下一步</button>
  </div>
</template>

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
