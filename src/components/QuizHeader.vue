<template>
  <header>
    <h4>Question {{quesStatus}}</h4>
    <div class="bar">
      <div class="completion" :style={width:barPercent}></div>
    </div>
  </header>
</template>
<script>
import { toRef } from "vue";
export default {
  props: {
    question: Array,
    questionStatus:String,
    barPercentage:String
  },
  setup(props) {
    const quesStatus = toRef(props, "questionStatus");
    const barPercent = toRef(props,"barPercentage")
    console.log("questionsquestions", quesStatus.value,barPercent.value);

    return {
      quesStatus,
      barPercent
    };
  },
};
</script>
<style scoped>
header {
  margin-top: 20px;
}
header h4 {
  font-size: 30px;
}
.bar {
  width: 300px;
  height: 50px;
  border: 3px solid bisque;
}
.completion {
  height: 100%;
  width: 0%;
  background-color: bisque;
}
</style>
