<template>
  <div>
    <h1>Vue Quiz App</h1>
    <QuestionQuiz v-if="currentQuestionIndex < questions.length"
    :questionData="questions[currentQuestionIndex]"
    @updateScore="updateScore"
    @nextQuestion="nextQuestion" />

    <ResultsQuiz v-if="currentQuestionIndex === questions.length"
    :score="score" :total="questions.length" />
  </div>
  
</template>

<script>
  import questions from "./questions.js";
  import QuestionQuiz from './components/QuestionQuiz.vue';
  import ResultsQuiz from './components/ResultsQuiz.vue';
import { onUpdated } from "vue";

  export default{
    components: {QuestionQuiz, ResultsQuiz},
    data() {
      return {
        questions,
        currentQuestionIndex: 0,
        score: 0
      };
    },
    methods: {
      updateScore(isCorrect) {
        if (isCorrect) {
          this.score++;
        }
      },
      nextQuestion() {
        this.currentQuestionIndex++;
      }
    }
  }
</script>