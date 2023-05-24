<script setup>

import {defineProps} from "vue"
import { useRouter } from "vue-router";


const router =useRouter()
const {quiz} = defineProps (['quiz'])



const navigateToQuiz = () =>
router.push(`/quiz/${quiz.id}`)

</script>








<template>
    <div>
        <div class="card" @click="navigateToQuiz">
            <img :src="quiz.img"
         alt="">
            <div class="card-text">
              <h2> {{quiz.name}}</h2>
              <p>{{quiz.questions.length}} questions</p>
            </div>
      
      
          </div>
    </div>
</template>


<style scoped>

.card{
    max-width:425px;
    border-radius:4px;
    background-color: antiquewhite;
    color:rgba(0, 0, 0, 0.774);
    border-top-left-radius: 0;
    border-top-right-radius: 0;
    overflow:hidden;
    border-radius:2%;
    box-shadow: 1px 1px 10px rgba(0,0,0,0.1);
    margin-bottom:35px;
    margin-right:20px;
    cursor:pointer;
  
  }
  
  .card img{
    width:100%;
    height:190px;
    margin:0;
  }
  
  .card-text{
    padding:8px;
  }
  
  .card h2{
    font-weight:bold;
  }



</style>