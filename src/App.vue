<template>
  <div>
    <ScorePanel />

    <template v-if="this.title">
      <h1 v-html="this.title"></h1>

      <template v-for="(answer, index) in this.answers" :key="index">
        <input v-model="this.chosenAnswer" type="radio" name="options" :value="answer"
          :disabled="this.answerSubmitted" />
        <label v-html="answer"></label><br />
      </template>

      <button class="send" type="button" v-if="!this.answerSubmitted" :disabled="!this.chosenAnswer"
        @click="this.sendAnswer()">Send</button>

      <section v-if="this.answerSubmitted" class="result">
        <h4 v-if="this.isChosenAnswerCorrect()">&#9989;
          Congratulations! The answer "<span v-html="this.correctAnswer"></span>"
          is correct!
        </h4>
        <h4 v-else>&#10060; I'm sorry, you picked the wrong answer.
          The correct is "<span v-html="this.correctAnswer"></span>"
        </h4>
        <button class="send" type="button" @click="this.getNewQuestion()">Next question</button>
      </section>

    </template>

  </div>
</template>

<script>

import ScorePanel from './components/ScorePanel.vue';
export default {
  name: 'App',
  components: {
    ScorePanel
  },

  data() {
    return {
      title: undefined,
      incorrectAnswers: [],
      correctAnswer: undefined,
      chosenAnswer: undefined,
      answerSubmitted: false,
    }
  },

  methods: {
    sendAnswer() {
      this.answerSubmitted = true;
    },
    isChosenAnswerCorrect() {
      return this.chosenAnswer == this.correctAnswer;
    },
    getNewQuestion() {

      this.answerSubmitted = false;
      this.chosenAnswer = undefined;
      this.title = undefined;

      const URL = "https://the-trivia-api.com/v2/questions?limit=1";
      this.axios
        .get(URL)
        .then((response) => {
          const question = response.data[0];
          this.title = question.question.text;
          this.incorrectAnswers = question.incorrectAnswers;
          this.correctAnswer = question.correctAnswer;
        })
    }
  },

  computed: {
    answers() {
      let answers = [...this.incorrectAnswers];
      answers.splice(Math.floor(Math.random() * answers.length), 0, this.correctAnswer);
      return answers;
    }
  },

  created() {
    this.getNewQuestion();
  }
}

</script>

<style lang="scss">
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin: 60px auto;
  max-width: 960px;

  input[type='radio'] {
    margin: 12px 4px;
  }

  button.send {
    margin-top: 12px;
    height: 40px;
    min-width: 120px;
    padding: 0 16px;
    color: #fff;
    background-color: #1867c0;
    border: 1px solid #1867c0;
    cursor: pointer;
  }

  button[disabled] {
    background-color: #6c6d6e;
    border: 1px solid #6c6d6e;
  }

}
</style>
