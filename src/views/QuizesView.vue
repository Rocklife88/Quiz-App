<script setup>
import q from "../data/Quizes.json"
import { ref, watch } from "vue"
import Card from "../components/Card.vue"


const quizes = ref(q)
const search = ref("")

watch(search, () => {
  quizes.value = q.filter(quiz => quiz.name.toLowerCase().includes(search.value.toLowerCase()))
})

</script>



<template>
  <div>
    <header>

      <h1>Quizes</h1>
      <input v-model.trim="search" type="text" placeholder="Search..." name="" id="">
    </header>
    <div class="cards-container">


      <Card v-for="quiz in quizes" :key="quiz.id" :quiz="quiz" />

    </div>

  </div>
</template>

<script setup>

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
  margin-right: 10px;
}

header input {
  border: none;
  background-color: rgb(128, 128, 128, 0.1);
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