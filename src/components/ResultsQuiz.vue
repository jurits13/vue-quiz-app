<template>
    <div class="resultsContainer">
      <h2>You've Completed The Quiz!</h2>
      <p>Your Score: {{ score }} / {{ total }}</p>
      <p>{{ finalMessage }}</p>

      <button class="retryButton" @click="restartQuiz">Try Again</button>
    </div>
</template>

<script>
export default {
    props: ["score", "total"],
    computed: {
        finalMessage() {
            if (this.score === this.total) {
                return "Perfect Score! 🎉 Well done!";
            } else if (this.score > this.total / 2) {
                return "Great job! You did well.";
            } else {
                return "Keep practicing!";
            }
        }
    },
    methods: {
        restartQuiz() {
            this.$emit("restartQuiz")
        }
    }
}
</script>

<style scoped>
.resultsContainer {
    display: flex;
    flex-direction: column;
    align-items: center;
    justify-content: flex-start;
    text-align: center;
    width: 100%;
    height: 100vh;
    padding-top: 10vh;
}

button {
    font-size: 1.5em;
    cursor: pointer;
    transition: 0.5s;
    background-color: white;
    color: black;
    border-radius: 0;
    border: 2px solid transparent;
    box-shadow: 0px 5px 10px rgb(210, 210, 210);
    margin-top: 3vh;
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
</style>