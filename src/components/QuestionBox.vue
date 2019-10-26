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
          :class="{selected:isSelected(index), correct:isCorrect(index)}"
        >
          <p>{{answer}}</p>
        </div>
      </div>
      <button @click="onSubmit">Save</button>
      <button @click="onNext">Next</button>
    </div>
  </section>
</template>
<script>
  import lodash from 'lodash';

  export default {
    props: {
      currentQuestion: Object,
      onNext: Function
    },
    data() {
      return {
        selectedItem: null,
        shuffledAnswers: [],
        correctIndex: null,
      }
    },
    watch: {
      currentQuestions: {
        immediate: true,
        handler() {

          this.selectedItem = null,
          this.shuffleAnswers()
        }
      }
    },
    computed: {
      answers() {
        return [
          ...this.currentQuestion.incorrect_answers,
           this.currentQuestion.correct_answer
         ];
      },
    },
    methods: {
      onSelect(index) {
        this.selectedItem = index;
      },
      onSubmit() {
        if (this.selectedItem === this.correctIndex) {
          this.selectedItem = null;
          //
        }
      },
      shuffleAnswers() {
        let answers = [
          ...this.currentQuestion.incorrect_answers,
           this.currentQuestion.correct_answer
         ];

         this.answers = lodash.shuffle(answers);
         this.correctIndex = this.answers.indexOf(this.currentQuestion.correct_answer);
      },
      isSelected(index) {
        return this.selectedItem === index ? true : false;
      },
      isCorrect(index){
        return index === this.correctIndex ? true : false;
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

  .correct {
    background-color: lightgreen;
  }


</style>
