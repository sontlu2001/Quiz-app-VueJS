<template>
  <div class="question">
    <h2 class="question-title">{{ question.title }}</h2>
    <ol class="options">
      <li
        v-for="answer in question.answers"
        :class="[
          'options-item',
          choosenAnswer ? (answer.isCorrect || false ? 'green' : 'red') : '',
        ]">
        <a href="#" @click="getAnswer(answer)">{{ answer.text }}</a>
      </li>
    </ol>
    <div v-if="choosenAnswer">
      <p :class="['answer', choosenAnswer.isCorrect ? 'correct' : 'incorrect']">
        <template v-if="choosenAnswer.isCorrect">Correct,</template>
        <template v-else>Incorrect, the correct answer is</template>
        {{ correctAnswer.text }}
      </p>
      <button @click="nextQuestion" class="btn">Next</button>
    </div>
  </div>
</template>

<script>
export default {
  name: "Question",

  props: {
    question: Object,
  },

  data() {
    return {
      choosenAnswer: null,
    };
  },

  watch: {
    question() {
      this.choosenAnswer = null;
    },
  },

  computed: {
    correctAnswer() {
      return this.question.answers.find((answer) => answer.isCorrect);
    },
  },

  methods: {
    getAnswer(answer) {
      if (this.choosenAnswer) {
        return;
      }
      this.choosenAnswer = answer;
    },

    nextQuestion() {
      this.$emit("nextQuestion", this.choosenAnswer);
    },
  },
};
</script>

<style>
.question-title {
  font-size: 20px;
  padding-bottom: 20px;
  margin-top: 20px;
  font-weight: 700;
}

.options-item a {
  position: relative;
  display: block;
  padding: 0.4em 0.4em 0.4em 2em;
  margin: 0.5em 0 0 20px;
  background: #dad2ca;
  color: #444;
  text-decoration: none;
  border-radius: 0.3em;
  transition: 0.3s ease-out;
  cursor: pointer;
}
.options-item a:hover {
  background: white;
}
.options-item a:hover:before {
  rotate: 360deg;
}
.options-item:first-child a:before {
  content: "A";
}
.options-item:nth-child(2) a:before {
  content: "B";
}
.options-item:nth-child(3) a:before {
  content: "C";
}
.options-item:nth-child(4) a:before {
  content: "D";
}
.options-item a:before {
  counter-increment: li;
  position: absolute;
  left: -1.3em;
  top: 50%;
  margin-top: -1.3em;
  background: #dad2ca;
  height: 2.6em;
  width: 2.6em;
  line-height: 2em;
  border: 0.3em solid #fff;
  text-align: center;
  font-weight: 700;
  border-radius: 2em;
  transition: all 0.3s ease-out;
}
.green a::before {
  background: #ad7;
}
.red a::before {
  background: #f49a74;
}
.correct {
  color: #ad7;
}
.btn {
  outline: none;
  border: none;
  cursor: pointer;
  background: #a0d8f3;
  padding: 10px 20px;
  border-radius: 4px;
  margin-top: 20px;
  font-size: 14px;
  color: white;
  font-weight: 600;
}
.answer {
  font-weight: 700;
}
.incorrect {
  color: #f49a74;
}
.correct {
  color: #ad7;
}
</style>
