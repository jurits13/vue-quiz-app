<template>
  <div class="questionContainer">
    <h2>{{ questionData.question }}</h2>
    <div class="optionsContainer"> 
        <button 
        v-for="option in questionData.options" 
        :key="option"
        @click = "selectAnswer(option)" 
        :disabled="selected !== null"
        :class="{correct:selected === option && isCorrect, incorrect: selected === option && !isCorrect}">
            {{ option }}
        </button>
    </div>
    <p v-if="selected"> {{ feedbackMessage }}</p>
    <button v-if="selected" @click="handleNextQuestion">Next</button>
  </div>
</template>

<script>
export default {
    props: ["questionData"],
    data() {
        return{
            selected: null,
            isCorrect: false
        }
    },
    computed: {
        feedbackMessage() {
            return this.isCorrect ? "Correct Answer!" : `Incorrect! The Correct Answer Was: ${this.questionData.answer}`
        }
    },
    methods: {
        selectAnswer(option) {
            this.selected = option
            this.isCorrect = option === this.questionData.answer
            this.$emit("updateScore", this.isCorrect)
        },
        handleNextQuestion() {
            this.$emit("nextQuestion")
            
            this.selected = null
            this.isCorrect = false
        }
    }
}
</script>

<style>
.questionContainer {
    padding: 20px;
    text-align: center;
    max-width: 500px;
    margin: auto;
}
.optionsContainer {
    display: grid;
    grid-template-columns: repeat(2, 1fr);
    grid-template-rows: repeat(2, 1fr);
    gap: 10px;
    justify-items: stretch;
}
button {
    cursor: pointer;
    transition: 0.5s;
}
button.correct {
    background-color: rgb(41, 201, 86);
    color: black;
}
button.incorrect {
    background-color: rgb(255, 74, 74);
    color: black;
}
</style>