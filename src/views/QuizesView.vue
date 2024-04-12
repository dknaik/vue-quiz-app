<template>
  <div>
    <header>
      <h1>Quizes</h1>
      <input v-model.trim="search" type="text" placeholder="Search..." />
    </header>
      <!-- v-for="quiz in quizes" :key="quiz.id" -->
      <!-- <div  class="card">
        <img :src="quiz.img" alt="" />
        <div class="card-text">
          <h2>{{ quiz.name }}</h2>
          <p>{{ quiz.questions.length }} questions</p>
        </div>
      </div> -->

      <!-- for animation -->
    <div class="options-container">
      <TransitionGroup appear @after-enter="afterEnter" @enter="enter" @before-enter="beforeEnter">
      <card  v-for="(quiz,index) in quizes" :key="quiz.id" :quiz="quiz" :data-index="index" />
      </TransitionGroup>
    </div>
  </div>
</template>
<script setup>
import q from "../fakers/quizes.json";
import Card from "../components/Card.vue";
import { ref, watch } from "vue";
import gsap from "gsap"
const quizes = ref(q);
const search = ref("");
watch(search, (newVal, oldVal) => {
  console.log(newVal, oldVal);
  quizes.value = q.filter((val) =>
    val.name.toLowerCase().includes(search.value.toLowerCase())
  );
});

const beforeEnter = (el)=>{
   console.log("before enter",el)
   el.style.opacity=0 
   el.style.transform = "translateY(-60px)"
}
const enter = (el)=>{
    console.log("entered",el.dataset.index)
  gsap.to(
    el,{
        y:0,
        opacity:1,
        duration:0.3, 
        delay:el.dataset.index * 0.3
    }
  )

}
const afterEnter = () =>{
    console.log("after entered")
}
</script>
<style scoped>
header {
  margin-bottom: 10px;
  margin-top: 30px;
  display: flex;
  align-items: center;
}
header h1 {
  font-weight: bold;
  margin-right: 30px;
}
header input {
  border: none;
  background-color: rgba(128, 128, 128, 0.1);
  padding: 10px;
  border-radius: 5px;
  outline: none;
}

/*Card styling */

.options-container {
  display: flex;
  flex-wrap: wrap;
  margin-top: 40px;
}

/*Animation */
/*.card-enter-from {
transform: translateY(-50px);
opacity: 0;
}
.card-enter-to {
transform: translateY(0);
opacity: 1;
}
.card-enter-active {
transition: all 0.4s ease;
} */
</style>

<!-- Transition life cycle events -->
<!-- before-enter
enter
after-enter
before-leave
leave
after-leave -->
