<template>
  <div>
    <h2>{{ questionData.question }}</h2>
    <div v-for="option in questionData.options" :key="option"> 
        <button @click = "selectAnswer(option)" :class="{correct:selected === option && isCorrect, incorrect: selected === option && !isCorrect}">
            {{ option }}
        </button>
    </div>
    <p v-if="selected"> {{ feedbackMessage }}</p>
    <button v-if="selected" @click="$emit('nextQuestion')">Next</button>
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
            return this.isCorrect ? "Correcto!" : "Incorrecto :("
        }
    },
    methods: {
        selectAnswer(option) {
            this.selected = option
            this.isCorrect = option === this.questionData.answer
            this.$emit("updateScore", this.isCorrect)
        }
    }
}
</script>