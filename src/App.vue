<template>
  <div id="app">
    <!-- 前测 -->
    <start @finish="saveInfo" v-if="step == 0"></start>
    <quesTable title="评估0-1" :list="ques01" @finish="saveQues" v-if="step == 1"></quesTable>
    <quesTable title="评估0-2" :list="ques02" @finish="saveQues" v-if="step == 2"></quesTable>
    <quesTable title="评估0-3" :list="ques03" @finish="saveQues" v-if="step == 3"></quesTable>
    <!-- 静坐 -->
    <slience @finish="step++" v-if="step == 4"></slience>
    <quesTable title="评估1-1" :list="SSAI" @finish="saveQues" v-if="step == 5"></quesTable>
    <quesTable title="评估1-2" :list="FAQS" @finish="saveQues" v-if="step == 6"></quesTable>
    <!-- A -->
    <template v-if="userInfo.group == 1">
      <english @finish="step++" v-if="step == 7"> </english>
      <quesTable title="A评估2-1" :list="SSAI" @finish="saveQues" v-if="step == 8"></quesTable>
      <quesTable title="A评估2-2" :list="FAQS" @finish="saveQues" v-if="step == 9"></quesTable>
      <breath @finish="step++" v-if="step == 10"></breath>
      <quesTable title="A评估3-1" :list="SSAI" @finish="saveQues" v-if="step == 11"></quesTable>
      <quesTable title="A评估3-2" :list="FAQS" @finish="saveQuesEnd" v-if="step == 12"></quesTable>
      <end @finish="init" v-if="step == 13"></end>
    </template>
    <!-- B -->
    <template v-if="userInfo.group == 2">
      <english @finish="step++" v-if="step == 7"> </english>

      <quesTable title="B评估2-1" :list="SSAI" @finish="saveQues" v-if="step == 8"></quesTable>
      <quesTable title="B评估2-2" :list="FAQS" @finish="saveQues" v-if="step == 9"></quesTable>
      <slience @finish="step++" v-if="step == 10"></slience>

      <quesTable title="B评估3-1" :list="SSAI" @finish="saveQues" v-if="step == 11">3-1</quesTable>
      <quesTable title="B评估3-2" :list="FAQS" @finish="saveQuesEnd" v-if="step == 12">3-2</quesTable>
      <end @finish="init" v-if="step == 13"></end>
    </template>
    <!-- c -->
    <template v-if="userInfo.group == 3">
      <breath @finish="step++" v-if="step == 7"> </breath>
      <quesTable title="C评估2-1" :list="SSAI" @finish="saveQues" v-if="step == 8"></quesTable>
      <quesTable title="C评估2-2" :list="FAQS" @finish="saveQues" v-if="step == 9"></quesTable>

      <english @finish="step++" v-if="step == 10"> </english>

      <quesTable title="C评估3-1" :list="SSAI" @finish="saveQues" v-if="step == 11">3-1</quesTable>
      <quesTable title="C评估3-2" :list="FAQS" @finish="saveQues" v-if="step == 12">3-2</quesTable>

      <slience @finish="step++" v-if="step == 13"></slience>

      <quesTable title="C评估4-1" :list="SSAI" @finish="saveQues" v-if="step == 14"></quesTable>
      <quesTable title="C评估4-2" :list="FAQS" @finish="saveQuesEnd" v-if="step == 15"></quesTable>
      <end @finish="init" v-if="step == 16"></end>
    </template>
  </div>
</template>

<script>
import quesTable from "./components/quesTable.vue";
import start from "./components/start.vue";
import end from "./components/end.vue";
import english from "./components/english.vue";
import slience from "./components/slience.vue";
import breath from "./components/breath.vue";

export default {
  name: "App",
  data() {
    return {
      step: 0,
      userInfo: {
        group: 2,
      },
      list: [],
      ques01: {
        name: "SIAS",
        thead: ["完全不符合", "有点符合", "比较符合", "非常符合", "完全符合"],
        list: [
          { q: "在必须与权威人士（老师、上司）谈话时，我感到紧张" },
          { q: "我感觉很难与他人有目光的接触" },
          { q: "如果我不得不谈论自己或自己的感受时，我会紧张" },
          { q: "我难以和我的同事/同学舒服地相处" },
          { q: "如果在街上碰到熟人，我会浑身紧张" },
          { q: "在社交场合我感到不舒服" },
          { q: "和另一个人单独在一起时，我会感到紧张" },
          { q: "我在聚会等社交场合很自在" },
          { q: "我和别人交谈感到有困难" },
          { q: "我觉得我能很容易找到可以谈论的话题" },
          { q: "我担心不能很好地表达我自己的意思会使自己出丑" },
          { q: "我发现对别人的观点表示不同意对我来说是一件困难的事情" },
          { q: "与有吸引力的异性交谈对我是困难的事情" },
          { q: "我发现自己担心在社交场合不知道该说些什么" },
          { q: "与不熟悉的人交往时，我感到紧张" },
          { q: "我觉得我在谈话中会说出一些令人尴尬的话来" },
          { q: "和一群人在一起的时候，我发现自己会担心被别人忽视" },
          { q: "和一群人在一起的时候，我觉得浑身紧张" },
          { q: "碰到一个不熟悉的人时我拿不准是否应该打招呼" },
        ],
      },
      ques02: {
        name: "FFMQ",
        thead: ["一点也不符合", "较少符合", "有些符合", "非常符合", "完全符合"],

        list: [
          { q: "走路时，我会细心地去体验我身体动起来的感觉" },
          { q: "我擅长用言语描述我的情感" },
          { q: "我会为自己有不理智、或不合适的情绪而责备自己" },
          { q: "我能随时感知我内心的丰富情感，但无需逐一对其作出反应" },
          { q: "我做事的时候常常走神，容易分心" },
          { q: "淋浴或沐浴时，我会特别留意水触摸我肌肤的感觉" },
          { q: "我能清晰表达自己的信念、观点以及期望" },
          { q: "我做事不专心因为我会胡思乱想，忧心忡忡，心不在焉" },
          { q: "我清楚我的心情是好是坏，但不至于为其纠结" },
          { q: "我会告诉自己，我不应该有此刻的这种感受" },
          { q: "我能意识到各种食物和饮品会如何影响我的身心状态" },
          { q: "我难以找到词语来表达我的所思所想" },
          { q: "我很容易分心" },
          { q: "我认为我的一些想法是异常的、不好的；我不应该那样想" },
          {
            q: "我会细心体验各种感觉，比如微风吹拂我的头发、阳光照在我的脸上的感觉",
          },
          { q: "我很难用合适的语言来表达我对事物的感受" },
          { q: "我经常评判自己的想法是好是坏" },
          { q: "我发现自己很难持续地将注意力集中到当下" },
          {
            q: "当我有令人不安的想法或意象时，我通常能退一步想一想，不会被其左右",
          },
          { q: "我会细心聆听各种声音，比如时钟滴答，鸟儿啾啾，行车飕飕" },
          { q: "遇到困境时，我通常能先冷静一下，不会冲动行事" },
          { q: "我很难找到合适的词语来描述我身体的各种感觉" },
          { q: "我似乎在无意识地自动运转，不太能清晰地意识到自己在做什么处" },
          { q: "当我有令人不安的想法或意象时，我通常能很快地恢复平静" },
          { q: "我会告诉我自己，我不应该有这样或那样的想法" },
          { q: "我能敏锐地觉察各种气味与芳香" },
          { q: "即使当我心情十分不好时，我也能找到词语来表达清楚是怎么回事" },
          { q: "我仓促地完成各项事情，实际上并未花多少心思" },
          {
            q: "当我有令人不安的想法或意象时，我通常能注意到它的存在，但不去对其作出反应",
          },
          { q: "我觉得我的一些情绪是不对的、不合时宜的、或者不应该有的" },
          {
            q: "我能敏锐地觉察艺术品和大自然里的视觉元素，譬如颜色，形状，纹理，光影等",
          },
          { q: "我擅长并能够用词语来清楚地描述我的体验" },
          { q: "当我有令人不安的想法或意象时，我通常只是觉察它们，顺其自然" },
          { q: "我机械地完成工作和任务，但实际上并不清楚自己正在做什么" },
          {
            q: "当我有令人不安的想法或意象时，我通常会根据想法的内容评判自己是好人还是坏人",
          },
          { q: "我常细心体会情绪如何影响我的思想和行为" },
          { q: "我通常能够非常详细地描述出我此刻的感受" },
          { q: "我觉得自己做事不专心" },
          { q: "当我有不理智的想法时，我会否定自己" },
        ],
      },
      ques03: {
        name: "FAQ",
        thead: ["从不", "偶尔", "有时", "大多数", "总是"],

        list: [
          { q: "在交流时我总是关注其他人的外表和穿着" },
          { q: "在交流时我总是关注周围环境的物理特征和条件（如外观和温度" },
          { q: "在交流时我总是关注下一步要说什么或下一步要做什么" },
          { q: "在交流时我总是关注我给他人留下的印象" },
          { q: "在交流时我总是关注他人怎样才能感受他们自己" },
          { q: "在交流时我总是关注他人的想法" },
          { q: "在交流时我总是关注我的焦虑水平" },
          { q: "在交流时我总是关注他人正在说什么和做什么" },
          { q: "在交流时我总是关注我的内部的身体反应（如，心律变化）" },
          { q: "在交流时我总是关注过去的社交失败经历" },
        ],
      },
      SSAI: {
        name: "SSAI",
        thead: ["完全没有", "有些", "中等程度", "非常明显"],

        list: [
          { q: "我感到心情平静" },
          { q: "我感到紧张" },
          { q: "我感到烦乱" },
          { q: "我感到轻松" },
          { q: "我感到心满意足" },
          { q: "我感到烦恼" },
        ],
      },
      FAQS: {
        name: "FAQ-S",
        thead: ["完全没有", "有些", "中等程度", "非常明显"],
        list: [
          { q: "如果我正在和他人交流，我总是会关注下一步要说什么或下一步要做什么" },
          { q: "如果我正在和他人交流，我总是会关注我给他人留下的印象" },
          { q: "如果我正在和他人交流，我总是会关注我的焦虑水平" },
          { q: "如果我正在和他人交流，我总是会关注我的内部的身体反应（如，心律变化）" },
          { q: "如果我正在和他人交流，我总是会关注过去的社交失败经历" },
        ],
      },
    };
  },
  components: {
    quesTable,
    start,
    end,
    english,
    slience,
    breath,
  },
  created() {
    document.onkeydown = (e) => {
      if (e.keyCode == 68 && e.ctrlKey) {
        e.preventDefault();
        this.step++;
      }
    };
  },
  methods: {
    init() {
      this.step = 0;
      this.userInfo = {};
      this.list = [];
    },
    saveInfo(info) {
      this.userInfo = info;
      this.step++;
    },
    saveQues(list) {
      this.list.push(list);
      this.step++;
    },
    saveQuesEnd(list) {
      this.list.push(list);
      this.step++;
      let saveItem = {
        userInfo: this.userInfo,
        list: this.list,
      };
      localStorage.setItem(+new Date() + "", JSON.stringify(saveItem));
      try {
        let allData = localStorage.getItem("allData");
        if (allData) {
          allData = JSON.parse(allData);
        } else {
          allData = [];
        }
        allData.push(saveItem);
        localStorage.setItem("allData", JSON.stringify(allData));
      } catch (e) {
        alert("存储失败，请联系管理员");
        console.error(e);
      }
    },
  },
};
</script>

<style>
#app {
  margin: 20px 300px;
  margin-top: 100px;
}
body,
html {
  /* color: white; */
  text-align: center;
  padding: 0;
  margin: 0;
}

#app h1 {
  color: #fff;
  font-size: 40px;
  margin-bottom: 40px;
}
#app h3 {
  font-size: 24px;
  margin-bottom: 40px;
}
#app h4 {
  font-size: 24px;
  margin-bottom: 10px;
}
#app p {
  text-align: center;
  font-size: 24px;
  margin-bottom: 40px;
  line-height: 40px;
}
#app .form-item {
  margin-bottom: 10px;
}
#app .form-item > span {
  display: inline-block;
  width: 80px;
}
#app thead {
  color: #fff !important;
  font-size: 14px !important;
}
</style>
