<template>
  <section class="question">
    <div class="question-wrap">
      <span class="category">{{currentQuestion.category}}</span>
      <h2>{{currentQuestion.question}}</h2>
      <div class="line"/>
      <div class="question-list">
        <div
          class="answer"
          v-for="(answer, index) in answers"
          :key="index"
          @click="onSelect(index)"
          :class="[selectedItem === index ? 'selected' : '']"
        >
          <p>{{answer}}</p>
        </div>
      </div>
      <button>Save</button>
      <button @click="onNext">Next</button>
    </div>
  </section>
</template>
<script>

Array.prototype.shuffle = function() {
  var i = this.length, j, temp;
  if ( i == 0 ) return this;
  while ( --i ) {
     j = Math.floor( Math.random() * ( i + 1 ) );
     temp = this[i];
     this[i] = this[j];
     this[j] = temp;
  }
  return this;
}

  export default {
    props: {
      currentQuestion: Object,
      onNext: Function
    },
    data() {
      return {
        selectedItem: ''
      }
    },
    computed: {
      answers() {
        let answers = [...this.currentQuestion.incorrect_answers];
        answers.push(this.currentQuestion.correct_answer);
        answers.shuffle;
        console.log(Array);
        return answers
      },
      correctAnswer() {
        return this.currentQuestion.correct_answer;
      }
    },
    methods: {
      onSelect(index) {
        this.selectedItem = index;
      }
    }
  }
</script>
<style type="scss" scoped>
  h2 {
    font-weight: normal;
    letter-spacing: 1px;
  }

  button {
      margin: 5px;
      height: 40px;
      width: 80px;
      background-color:
  }

  .category {
    color: #6f7f94;
    font-size: 16px;
    font-style: italic;
  }

  .question-wrap {
    margin-top: 20px;
    text-align: center;
  }

  @media(min-width: 800px) {
    .question-wrap {
      max-width: 50%;
    }
  }

  @media(max-width: 800px) {
    h2 {
      font-size: 19px;
    }
  }

  .question {
    padding: 15px;
    display: flex;
    justify-content: center;
  }

  .question-list {
    margin-top: 30px;
  }

  .answer {
    margin: 2px;
    border: 1px solid rgba(0,0,0,.1);
    border-radius: 5px;
  }

  .answer:hover {
    background-color: #eee;
  }

  .selected {
    background-color: #eee;
  }


</style>
