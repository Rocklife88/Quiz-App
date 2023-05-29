<script setup>
import q from "../data/Quizes.json";
import { ref, watch } from "vue";
import { TransitionGroup } from "vue";

import Card from "../components/Card.vue";
import gsap from "gsap";

const quizes = ref(q);
const search = ref("");

watch(search, () => {
  quizes.value = q.filter((quiz) =>
    quiz.name.toLowerCase().includes(search.value.toLowerCase())
  );
});

const beforeEnter = (el) => {
  el.style.opacity = 0;
  el.style.transform = "translateY(-100px)";
};

const enter = (el) => {
  gsap.to(el, {
    y: 0,
    opacity: 1,
    duration: 0.2,
    delay: el.getAttribute("data-index") * 0.3,
  });
};

const afterEnter = (el) => {
  el.style.opacity = "";
  el.style.transform = "";
};
</script>



<template>
  <div>
    <header>
      <h1>Quizzes</h1>
      <input v-model.trim="search" type="text" placeholder="Search..." />
    </header>
    <div class="cards-container">
      <TransitionGroup appear @before-enter="beforeEnter" @enter="enter" @after-enter="afterEnter">
        <Card v-for="(quiz,index) in quizes" 
        :key="quiz.id" 
        :quiz="quiz" 
        :data-index="index"
        />
      </TransitionGroup>
    </div>
  </div>
</template>

<style scoped>
header {
  margin-bottom: 10px;
  margin-top: 30px;
  display: flex;
  align-items: center;
}

header h1 {
  font-weight: bold;
  margin-right: 10px;
}

header input {
  border: none;
  background-color: rgba(128, 128, 128, 0.1);
  padding: 15px;
  border-radius: 5px;
  width: 250px;
}

.cards-container {
  display: flex;
  flex-wrap: wrap;
  margin-top: 40px;
}

</style>
