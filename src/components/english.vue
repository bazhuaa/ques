<template>
  <div class="eng">
    <div v-if="step == 0">
      <h1>全国英语演讲比赛</h1>
      <p>
        指导语：<br />
        下面，你有1分钟的时间准备一段关于“我理想的职业”主题的英文讲稿<br />
        倒计时结束后，将做3分钟的口头演讲，并接受现场专家的提问<br />
        专家将根据你的现场表现进行评分
      </p>

      <button class="btn btn-info" @click="knowIt">我已知晓 {{ readTime }}s</button>
    </div>

    <div v-if="step == 1">
      <h1>National English Speaking Competition</h1>
      <h4>My Ideal Job</h4>
      <div style="height: 30px; border-bottom: 1px solid #ccc"></div>
      <div style="height: 30px; border-bottom: 1px solid #ccc"></div>
      <div style="height: 30px; border-bottom: 1px solid #ccc"></div>
      <div style="height: 30px; border-bottom: 1px solid #ccc; margin-bottom: 20px"></div>
      <button class="btn btn-success">倒计时{{ thinkTime }}s</button>
    </div>

    <div v-if="step == 2">
      <h1>National English Speaking Competition</h1>
      <h3>Your Speech</h3>
      <button class="btn btn-success">倒计时{{ speechTime }}s</button>
    </div>
  </div>
</template>

<script>
export default {
  name: "quesTable",
  props: {},
  data() {
    this.readTimer = null;
    this.thinkTimer = null;
    this.speechTimer = null;
    return {
      step: 0,
      readTime: 30,
      thinkTime: 60, //todo 60
      speechTime: 180, //todo 180
    };
  },
  methods: {
    nextStep() {
      this.$emit("finish");
    },
    knowIt() {
      this.step++;
      clearInterval(this.readTimer);
      this.thinkTimer = setInterval(() => {
        this.thinkTime--;
        if (this.thinkTime == 0) {
          this.step++;
          clearInterval(this.thinkTimer);
          this.speechTimer = setInterval(() => {
            this.speechTime--;
            if (this.speechTime == 0) {
              this.nextStep();
              clearInterval(this.speechTimer);
            }
          }, 1000);
        }
      }, 1000);
    },
  },
  created() {
    this.readTimer = setInterval(() => {
      this.readTime--;
      if (this.readTime == 0) {
        this.knowIt();
      }
    }, 1000);
  },
};
</script>

<style scoped>
.eng {
  padding-top: 60px;
}
</style>
