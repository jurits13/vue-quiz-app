<template>
  <div class="questionContainer">
    <h2>{{ questionData.question }}</h2>
    <div class="optionsWrapper">
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
    </div>
    
    <div class="feedbackContainer">
        <p v-if="selected"> {{ feedbackMessage }}</p>
        <button v-if="selected" class="nextButton" @click="handleNextQuestion">Next</button>
    </div>
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
            return this.isCorrect ? "Correct answer!" : `Incorrect! The correct answer was: ${this.questionData.answer}`
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

<style scoped>
.questionContainer {
    padding: 20px;
    text-align: center;
    width: 100%;
    max-width: 100%;
    margin-top: 6vh;
    align-items: center;
}
.optionsContainer {
    display: grid;
    grid-template-columns: repeat(2, minmax(120px, 1fr)); 
    grid-template-rows: repeat(2, minmax(100px, auto)); 
    gap: 15px;
    justify-items: center;
    width: 100%;
    max-width: 1200px;
    margin: 0 auto;
    padding: 0 10px;
    box-sizing: border-box;
}
.optionsWrapper {
    background-color: rgb(244, 244, 244);
    padding: 2em;
    display: flex;
    justify-content: center;
    justify-items: center;
    width: 100%;
    max-width: 100%;
    margin: 0 auto;
    box-sizing: border-box;
    margin-top: 4vh;
}
.feedbackContainer {
    height: 200px;
    display: flex;
    flex-direction: column;
    align-items: center;
    justify-content: center;
}
button {
    font-size: 1.5em;
    width: 100%;
    height: 20vh;
    cursor: pointer;
    transition: 0.5s;
    background-color: white;
    color: black;
    border-radius: 2px;
    border: 2px solid transparent;
    box-shadow: 0px 5px 10px rgb(231, 231, 231);
}
button:hover {
    background-color: black;
    color: white;
    outline: none;
    transform: scale(1.05);
    outline: none !important;
    border: none !important;
    box-shadow: none !important;
}
button.correct {
    background-color: rgb(98, 255, 142);
    color: black;
}
button.incorrect {
    background-color: rgb(255, 74, 74);
    color: black;
}
button.nextButton {
    margin-top: 20px;
    padding: 20px 20px;
    width: 30vw;
    height: 10vh;
    text-align: center;
}
button.disabled {
    opacity: 0.5;
    cursor: not-allowed;
    pointer-events: none
}

@media screen and (max-width: 700px) {
    .optionsContainer {
        grid-template-columns: 1fr;
    }
    button {
    height: 15vh;
    }
    .optionsWrapper {
        padding: 1em;
    }
}

</style>