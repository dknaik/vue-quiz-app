<template>
  <div class="results">
    <p>Your Results...</p>
    <h1>{{noOfCorrectAns}}/{{questLen}}</h1>
    <RouterLink to="/">Go Back</RouterLink>
  </div>
</template>
<script>
import { toRef } from 'vue';
    import {RouterLink} from "vue-router"
export default {
  props: {
    questionLength: {
      type: String,
    },
    noOfCorrectAns: {
      type: String,
    },
  },

  setup(props) {
    const questLen = toRef(props, "questionLength");
    const noOfCorrectAns = toRef(props, "noOfCorrectAns");
    console.log("questLen",questLen.value,noOfCorrectAns.value)
    return { questLen, noOfCorrectAns };
  },
};
</script>

<style scoped>
.results {
  text-align: center;
  padding: 100px 0;
}
p {
  font-size: 25px;
}
h1 {
  font-size: 80px;
}
</style>
