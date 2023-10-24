<template>
  <div id="app">
    <article>
      <header>
        <h1 class="title">Quiz Test</h1>
      </header>
      <template v-if="!isEnd">
        <section>
          <p>
            Question {{ currentQuestion + 1 }} out of {{ questions.length }}
          </p>
          <Question
            :question="questions[currentQuestion]"
            @nextQuestion="nextQuestion" />
        </section>
      </template>
      <template v-else>
        <Result :result="result" />
      </template>
    </article>
  </div>
</template>

<script>
import Question from "./components/Question.vue";
import Result from "./components/Result.vue";

export default {
  name: "App",
  components: {
    Question,
    Result,
  },
  data() {
    return {
      questions: [
        {
          title: "What is CSS?",
          answers: [
            { text: "Controlled Sporadic Spasms" },
            { text: "Critical Stylish Severity" },
            { text: "Cascading Style Sheets", isCorrect: true },
          ],
        },
        {
          title: "What is not a front-end  tool?",
          answers: [
            { text: "Webpack" },
            { text: "Tortilla", isCorrect: true },
            { text: "Gulp" },
          ],
        },
        {
          title: "What is an HTML tag for an ordered list?",
          answers: [
            { text: "<ol>", isCorrect: true },
            { text: "<list>" },
            { text: "<ul>" },
          ],
        },
      ],
      currentQuestion: 0,
      correctAnswers: 0,
    };
  },
  computed: {
    isEnd() {
      return this.currentQuestion >= this.questions.length;
    },
    result() {
      return Math.round((this.correctAnswers / this.questions.length) * 100);
    },
  },
  methods: {
    nextQuestion(answer) {
      if (answer.isCorrect) {
        this.correctAnswers++;
      }
      this.currentQuestion++;
    },
  },
};
</script>

<style>
.options {
  padding-left: 0px;
}

article {
  background: #313536;
  padding: 20px 40px 100px;
  border-radius: 4px;
  max-width: 500px;
  min-height: 470px;
  margin: 0 auto;
}
.title {
  font-size: 25px;
  text-align: center;
  font-family: "Arial Black";
  color: #a0d8f3;
  margin: 25px 0;
}
</style>
