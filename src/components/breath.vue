<template>
  <div class="hello">
    <h1>正念呼吸</h1>
    <p>
      指导语： <br />下面请跟随音频 调节你的呼吸和身体状态。<br />
      请花点时间，感觉一下。<br />
      {{ timeBefore == 0 ? "" : "10秒后开始播放正念音频" }}
      {{ timeBefore ? "（" + timeBefore + "s）" : "" }}
    </p>
    <div style="position: relative; width: 300px; margin: 0 auto">
      <audio
        style="margin: 10px auto; display: block !important"
        height="100"
        width="100"
        ref="audio"
        id="audio"
      >
        <source src="breath.mp3" type="audio/mpeg" />
        <embed height="50" width="100" src="breath.mp3" />
      </audio>
      <span style="margin-right: 10px">{{ audioStr }}/9:24</span>
      <progress class="progress w-56" :value="audioT / 564"></progress>
      <div
        style="
          position: absolute;
          left: 0;
          top: 0;
          width: 35px;
          height: 54px;
          background-color: #000;
          z-index: 1;
        "
      ></div>
      <div
        style="
          position: absolute;
          right: 0;
          top: 0;
          width: 35px;
          height: 54px;
          background-color: #000;
          z-index: 1;
        "
      ></div>
    </div>

    <button @click="nextStep" class="btn btn-success" v-show="end">
      下一步{{ end ? "（" + timeAfter + "s）" : "" }}
    </button>
    <audio src="Abreath.mp3" autoplay v-if="group == 'A'"></audio>
    <audio src="Cbreath.mp3" autoplay v-if="group == 'C'"></audio>
  </div>
</template>
margin: 0 auto;

<script>
export default {
  name: "quesTable",
  props: { group: {} },
  data() {
    this.timer = null;
    this.audioTimer = null;
    return {
      timeBefore: 10,
      timeAfter: 10,
      end: false,
      audioT: 0,
    };
  },
  methods: {
    nextStep() {
      this.$emit("finish");
    },
  },
  created() {
    if (this.group == "C") {
      this.timeBefore = 12;
    }
    this.timer = setInterval(() => {
      this.timeBefore--;
      if (this.timeBefore == 0) {
        this.$refs["audio"].play();
        this.audioTimer = setInterval(() => {
          this.audioT++;
          if (this.audioT == 564) {
            clearInterval(this.audioTimer);
          }
        }, 1000);
        clearInterval(this.timer);
      }
    }, 1000);
  },
  computed: {
    audioStr() {
      let b = Math.floor(this.audioT / 60);
      let a = (this.audioT % 60) + "";
      if (a.length <= 1) {
        a = "0" + a;
      }
      return `${b}:${a}`;
    },
  },
  mounted() {
    let audio = document.getElementById("audio");
    audio.addEventListener("ended", () => {
      //todoended
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
