<template>
  <div id="app">
    <Header :points="points" :total="total"/>
    <QuestionSelect v-if="amount === index" :getQuestions="getQuestions"/>
    <QuestionBox
      v-if="questions.results.length && amount > index"
      :currentQuestion="questions.results[index]"
      :onNext="onNext"
      :addPoints="addPoints"
    />
  </div>
</template>

<script>
import Header from './components/Header.vue';
import QuestionBox from './components/QuestionBox.vue';
import QuestionSelect from './components/QuestionSelect.vue';

const API_URL = 'https://opentdb.com/api.php?';

export default {
  name: 'app',
  components: {
    Header,
    QuestionBox,
    QuestionSelect
  },
  data() {
    return {
      questions: [],
      amount: 10,
      index: 0,
      points: 0,
      total: 0
    }
  },
  mounted: function() {
    this.getQuestions()
  },
  methods: {
    onNext() {
      this.index++;
    },
    addPoints(correctAnswer) {
      if (correctAnswer) {
        this.points++;
      }

      this.total++;
    },
    getQuestions() {
      fetch(API_URL + 'amount=' + this.amount, {
        method: 'get'
      })
      .then((response) => {
        return response.json();
      })
      .then((jsonData) => {
        this.questions = jsonData;
      })
    }
  }
}
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  color: #2c3e50;
}

.line {
  width: 100%;
  height: 0px;
  border-bottom: 1px solid rgba(0,0,0,.1);
}

.question {
  padding: 15px;
  display: flex;
  justify-content: center;
}
</style>
