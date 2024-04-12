<template>
  <div class="card" @click="navigateToQuiz(quizData)">
    <img
      :src="quizData.img"
      alt=""
    />
    <div class="card-text">
      <h2>{{quizData.name}}</h2>
      <p>{{quizData.questions.length}} Questions</p>
    </div>
  </div>
</template>
<script>
import { toRef } from "vue";
import {useRouter} from "vue-router"

export default {
  props: {
    quiz: {
      type: String,
    },
  },
  setup(props) {
    const quizData = toRef(props, "quiz");
    console.log("quizData",quizData)
    const router = useRouter()
    const navigateToQuiz= (quizData) =>{
      router.push(`/quiz/${quizData.id}`)
    }
    return {
        quizData,
        navigateToQuiz
    }
  },
};
</script>
<style scoped>
.card {
  width: 310px;
  overflow: hidden;
  border-radius: 2%;
  box-shadow: 1px 1px 10px rgba(0, 0, 0, 0.1);
  margin-bottom: 35px;
  margin-right: 30px;
  cursor: pointer;
}
.card img {
  width: 100%;
  height: 190px;
}
.card .card-text {
  padding: 0 5px;
}
.card .card-text h2 {
  font-weight: bold;
}
</style>
