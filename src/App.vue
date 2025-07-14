<template>
  <div>
    <h1 v-html="this.title"></h1>

    <input type="radio" name="options" value="True" />
    <label>True</label><br />

    <input type="radio" name="options" value="False" />
    <label>False</label><br />

    <button class="send" type="button">Send</button>

  </div>
</template>

<script>

export default {
  name: 'App',

  data() {
    return {
      title: undefined,
      incorrectAnswers: undefined,
      correctAnswer: undefined
    }
  },

  created() {
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
}

// 
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

}
</style>
