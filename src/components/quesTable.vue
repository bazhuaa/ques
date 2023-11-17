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
                <input v-model="outArr[index]" type="radio" :value="headIndex" class="radio" />
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
    <button class="btn btn-info" @click="nextStep" type="normal">下一步</button>
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
    };
  },
  methods: {
    nextStep() {
      let noComplete = this.list.list.some((i, index) => {
        // this.outArr[index] = 1; //todo
        if (!this.outArr[index]) {
          return true;
        }
      });
      if (noComplete) {
        alert("还有未完成的选项");
        return;
      }
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
