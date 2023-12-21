<template>
  <div class="hello">
    <h1>实验结束，感谢您的参与！</h1>
    <p>请取下生理设备，填写被试单并领取被试费</p>
    <button @click="nextStep" class="btn btn-info">重新开始</button>
    <button
      style="right: 5px; bottom: 5px; position: absolute"
      @click="output"
      class="btn"
    >
      导出
    </button>
    <audio src="end.mp3" autoplay></audio>
  </div>
</template>

<script>
export default {
  name: "quesTable",
  props: {},
  methods: {
    nextStep() {
      this.$emit("finish");
    },
    output() {
      let allData = localStorage.getItem("allData");
      if (allData) {
        allData = JSON.parse(allData);
        // console.log(allData);
      } else {
        allData = [];
      }
      // [{"userInfo":{"group":2},"list":[{"name":"FAQ-S","stage":"B评估3-2","list":[1,1,1,1,1]}]}]
      let res = [];
      allData.map((i) => {
        let { userInfo, list } = i;
        let obj = {
          编号: userInfo.No,
          性别: userInfo.age,
          英语水平: userInfo.engLevel,
          性别: userInfo.gender,
          组别: userInfo.group,
          正念水平: userInfo.mindfulLevel,
        };
        list.forEach((l) => {
          l.list.forEach((ques, index) => {
            console.log(l.stage + "-" + index, ques);
            obj[l.stage + "-" + index] = ques;
          });
        });
        res.push({ ...obj });
      });

      const wb = XLSX.utils.book_new();
      const ws = XLSX.utils.json_to_sheet(res, { dense: true });
      XLSX.utils.book_append_sheet(wb, ws);
      XLSX.writeFile(wb, `${new Date().toLocaleTimeString()}.xlsx`, {
        bookSST: true,
      });
    },
  },
};
</script>

<style scoped></style>
