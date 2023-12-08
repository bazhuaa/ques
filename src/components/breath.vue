<template>
  <div class="hello">
    <h1>正念呼吸</h1>
    <p>
      指导语： <br />下面请跟随音频 调节你的呼吸和身体状态。<br />
      请花点时间，感觉一下。<br />
      10秒后开始播放正念音频{{ timeBefore ? "（" + timeBefore + "s）" : "" }}
    </p>
    <div>
      <audio style="margin: 10px auto" controls height="100" width="100" ref="audio" id="audio">
        <source src="breath.mp3" type="audio/mpeg" />
        <embed height="50" width="100" src="breath.mp3" />
      </audio>
    </div>
    <button @click="nextStep" class="btn btn-success" v-show="end">
      下一步{{ end ? "（" + timeAfter + "s）" : "" }}
    </button>
  </div>
</template>
margin: 0 auto;

<script>
export default {
  name: "quesTable",
  props: {},
  data() {
    this.timer = null;
    return {
      timeBefore: 10,
      timeAfter: 10,
      end: false,
    };
  },
  methods: {
    nextStep() {
      this.$emit("finish");
    },
  },
  created() {
    this.timer = setInterval(() => {
      this.timeBefore--;
      if (this.timeBefore == 0) {
        this.$refs["audio"].play();
        clearInterval(this.timer);
      }
    }, 1000);
  },
  mounted() {
    let audio = document.getElementById("audio");
    audio.addEventListener("ended", () => {
      this.end = true;
      this.timer = setInterval(() => {
        this.timeAfter--;
        if (this.timeAfter == 0) {
          this.$emit("finish");

          clearInterval(this.timer);
        }
      }, 1000);
    });
  },
  beforeDestroy() {
    clearInterval(this.timer);
  },
};
</script>

<style scoped></style>
