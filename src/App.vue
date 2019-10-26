<template>
  <div id="app">
    <Header />
    <QuestionBox v-if="questions.results.length" :currentQuestion="questions.results[index]" :onNext="onNext" />
  </div>
</template>

<script>
import Header from './components/Header.vue'
import QuestionBox from './components/QuestionBox.vue'

const API_URL = 'https://opentdb.com/api.php?';

export default {
  name: 'app',
  components: {
    Header,
    QuestionBox
  },
  data() {
    return {
      questions: [],
      index: 0,
    }
  },
  mounted: function() {
    fetch(API_URL + 'amount=10', {
      method: 'get'
    })
    .then((response) => {
      return response.json();
    })
    .then((jsonData) => {
      this.questions = jsonData;
    })
  },
  methods: {
    onNext() {
      this.index++;
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
</style>
