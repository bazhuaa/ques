<template>
  <div class="hello">
    <div v-if="step == 0">
      <h1 style="font-size: 50px">你好，欢迎参加本实验</h1>
      <h3 @click="step++" style="cursor: pointer">（点击进入实验程序）</h3>
    </div>
    <div v-if="step == 1">
      <h3>参与者信息</h3>
      <div style="text-align: left">
        <div class="form-item">
          <span>编号：</span>
          <input v-model="form.No" type="text" class="input input-bordered w-full max-w-xs" />
        </div>
        <div class="form-item">
          <span>性别：</span>
          <select v-model="form.gender" class="select select-bordered">
            <option value="1">男</option>
            <option value="2">女</option>
          </select>
        </div>
        <div class="form-item">
          <span>组别：</span>
          <select v-model="form.group" class="select select-bordered">
            <option value="1">A</option>
            <option value="2">B</option>
            <option value="3">C</option>
          </select>
        </div>
        <div class="form-item">
          <span>年龄：</span>
          <input v-model="form.age" type="text" class="input input-bordered w-full max-w-xs" />
        </div>
        <div class="form-item">
          <span>英语水平：</span>
          <input v-model="form.engLevel" type="text" class="input input-bordered w-full max-w-xs" />
        </div>
        <div class="form-item">
          <span>正念水平：</span>
          <select v-model="form.mindfulLevel" class="select select-bordered">
            <option value="1">新手</option>
            <option value="2">正念者</option>
          </select>
        </div>
      </div>
      <button class="btn btn-info" @click="validate">开始</button>
    </div>
    <div v-if="step == 2">
      <video></video>

      <button class="btn btn-info" @click="nextStep">下一步</button>
    </div>
  </div>
</template>

<script>
export default {
  name: "quesTable",
  props: {},
  data() {
    return {
      step: 0,
      form: {
        No: "",
        group: "",
        gender: "",
        mindfulLevel: "",
        age: "",
        engLevel: "",
      },
    };
  },
  methods: {
    validate() {
      let hasNull = Object.values(this.form).some((v) => !v);
      if (hasNull) {
        alert("请输入完整信息");
      } else {
        this.step++;
      }
    },
    nextStep() {
      this.$emit("finish", this.form);
    },
  },
};
</script>

<style scoped></style>
