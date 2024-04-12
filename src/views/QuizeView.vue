<template>
  <div>
    <quiz-header
      :question="question"
      :questionStatus="questionStatus"
      :barPercentage="barPercentage"
    />
    <div>
      <question
        v-if="!showResults"
        :question="quest?.questions[currentQuestionIndex]"
        @selectedOption="onOptionSelected"
      />
      <Result
        v-else
        :questionLength="quest.questions.length"
        :noOfCorrectAns="totalCorrectAns"
      />
    </div>
  </div>
</template>
<script>
import Question from "../components/Question.vue";
import QuizHeader from "../components/QuizHeader.vue";
import { useRoute } from "vue-router";
import Result from "../components/Result.vue";
import q from "../fakers/quizes.json";
import { computed, ref, watch } from "vue";

export default {
  components: { Question, QuizHeader, Result },
  setup() {
    const route = useRoute();
    const quizId = parseInt(route.params.id);
    const quest = q.find((question) => question.id == quizId);
    console.log("question", quest);
    const currentQuestionIndex = ref(0);
    const totalCorrectAns = ref(0);
    const showResults = ref(false);
    // const nextQustion = () => {
    //   currentQuestionIndex.value = currentQuestionIndex.value + 1;
    // };
    const onOptionSelected = (value) => {
      console.log("value", value);
      if (value) {
        totalCorrectAns.value++;
      }
      if (currentQuestionIndex.value === quest.questions.length - 1) {
        showResults.value = true;
      }
      currentQuestionIndex.value++;
    };
    // const questionStatus = ref(`${currentQuestionIndex.value}/${quest.questions.length}`);
    // watch(
    //   () => currentQuestionIndex.value,
    //   () => {
    //     questionStatus.value = `${currentQuestionIndex.value}/${quest.questions.length}`;
    //   }
    // );
    const questionStatus = computed(() => {
      return `${currentQuestionIndex.value}/${quest.questions.length}`;
    });
    const barPercentage = computed(
      () => `${(currentQuestionIndex.value / quest.questions.length) * 100}%`
    );
    return {
      q,
      quest,
      currentQuestionIndex,
      questionStatus,
    //   nextQustion,
      barPercentage,
      onOptionSelected,
      showResults,
      totalCorrectAns
    };
  },
};
</script>

<style scoped></style>
