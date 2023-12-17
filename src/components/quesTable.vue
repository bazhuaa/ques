<template>
  <div class="hello">
    <h4>{{ title }}（{{ list.name }}）</h4>
    <table class="table">
      <!-- head -->
      <thead>
        <tr>
          <th v-for="item in list.thead">{{ item }}</th>
        </tr>
      </thead>
    </table>
    <div class="overflow-x-auto" style="height: 550px">
      <table class="table">
        <!-- head -->
        <!-- <thead>
          <tr>
            <th>完全不符合</th>
            <th>有点符合</th>
            <th>比较符合</th>
            <th>非常符合</th>
            <th>完全符合</th>
          </tr>
        </thead> -->
        <tbody>
          <template v-for="(item, index) in list.list">
            <tr>
              <th colspan="5">{{ index + 1 + "、" + item.q }}</th>
            </tr>
            <tr>
              <th v-for="(head, headIndex) in list.thead">
                <input
                  v-model="outArr[index]"
                  type="radio"
                  :value="headIndex + 1"
                  class="radio"
                />
              </th>

              <!-- <td><input v-model="outArr[index]" type="radio" value="2" class="radio" /></td>
              <td><input v-model="outArr[index]" type="radio" value="3" class="radio" /></td>
              <td><input v-model="outArr[index]" type="radio" value="4" class="radio" /></td>
              <td><input v-model="outArr[index]" type="radio" value="5" class="radio" /></td> -->
            </tr>
          </template>
        </tbody>
      </table>
    </div>
    <button class="btn btn-info" type="normal" @click="nextStep">
      倒计时{{ time }}s
    </button>
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
    return {
      outArr: [],
      timer: null,
      time: 50,
    };
  },
  created() {
    //滴一声
    if (this.list.list.length >= 15) {
      this.time = 100;
    }
    if (this.list.list.length >= 30) {
      this.time = 150;
    }
    // 30秒
    this.timer = setInterval(() => {
      if (this.time == 0) {
        this.nextStep();
        clearInterval(this.timer);
      }
      this.time--;
    }, 1000);
  },
  beforeDestroy() {
    this.timer = null;
  },
  methods: {
    nextStep() {
      // let noComplete = this.list.list.some((i, index) => {
      //   // this.outArr[index] = 1; //todo
      //   if (!this.outArr[index]) {
      //     return true;
      //   }
      // });
      // if (noComplete) {
      //   alert("还有未完成的选项");
      //   return;
      // }
      this.$emit("finish", {
        name: this.list.name,
        stage: this.title,
        list: this.outArr,
      });
      this.outArr = [];
    },
  },
};
</script>

<style scoped></style>
