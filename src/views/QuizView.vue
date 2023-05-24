<script setup>
import Question from "../components/Question.vue"
import Results from "../components/Results.vue"
import Header from "../components/Header.vue"
import { useRoute } from "vue-router";
import {ref, watch, computed} from "vue";
import quizes from "../data/Quizes.json"

const route= useRoute()
const quizId= parseInt(route.params.id)
const quiz = quizes.find(q => q.id ===quizId)
const currentQuestionIndex= ref(0)
const numberOfCorrectAnswers = ref(0)
const showResults =ref(false)

const questionStatus =computed(()=> `${currentQuestionIndex.value}/${quiz.questions.length}`)
const barPercentage = computed(()=>  `${currentQuestionIndex.value/quiz.questions.length *100}%`)
const onOptionSelected = (isCorrect) => {
if (isCorrect) {
    numberOfCorrectAnswers.value++;

}
if(quiz.questions.length-1 === currentQuestionIndex.value) {
    showResults.value = true

}
currentQuestionIndex.value++
}




</script>



<template>
    <div>
        <Header
        :questionStatus="questionStatus"
        :barPercentage="barPercentage"
        
        />
        </div>
        
        <div>
         <Question  v-if="!showResults"
                   :question="quiz.questions[currentQuestionIndex]"
                    @selectOptions="onOptionSelected"
                    />
<Results 
v-else
:quizQuestionLength = "quiz.questions.length"
:numberOfCorrectAnswers = "numberOfCorrectAnswers"


/>
            </div>
            <!-- <button @click="currentQuestionIndex++">Next question</button> -->

</template>



