<template>
  <div class="hello">
    <h4>{{ title }}（{{ list.name }}）</h4>
    <p>
      请阅读以下六项表述，思考在刚刚的正念练习中有多长时间您的体验与该项表述一致，并进行0%-100%的打分，其中0%代表完全不一致，100%代表完全一致。
    </p>
    <div class="overflow-x-auto" style="height: 550px">
      <table class="table">
        <tbody>
          <template v-for="(item, index) in list.list">
            <tr>
              <th>{{ index + 1 + "、" + item.q }}</th>
            </tr>
            <tr>
              <th>
                <span>{{ outArr[index] || 0 }}%</span>
                <input
                  type="range"
                  min="0"
                  max="100"
                  class="range range-xs range-accent"
                  v-model="outArr[index]"
                />
              </th>
            </tr>
          </template>
        </tbody>
      </table>
    </div>
    <button class="btn btn-success">倒计时{{ time }}s</button>
    <audio src="di.mp3" autoplay></audio>
  </div>
</template>

<script>
export default {
  name: "quesTable",
  props: {
    list: {},
    title: {},
  },
  data() {
    return { timer: null, time: 60, outArr: [] }; //todo 60
  },
  methods: {
    nextStep() {
      this.$emit("finish", {
        name: this.list.name,
        stage: this.title,
        list: this.outArr,
      });
      this.outArr = [];
    },
  },
  created() {
    // 30秒
    this.timer = setInterval(() => {
      if (this.time == 0) {
        this.nextStep();
        clearInterval(this.timer);
      }
      this.time--;
    }, 1000);
    this.outArr = new Array(this.list.list.length).fill(50);
  },
  beforeDestroy() {
    this.timer = null;
  },
};
</script>

<style scoped></style>
