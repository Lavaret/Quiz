<template>
  <section class="question">
    <div class="question-wrap">
      <span class="category">{{currentQuestion.category}}</span>
      <h2>{{currentQuestion.question | refactor}}</h2>
      <div class="line"/>
      <div class="question-list" :class="{submitted:submitted}">
        <div
          class="answer"
          v-for="(answer, index) in shuffledAnswers"
          :key="index"
          @click="onSelect(index)"
          :class="{
              selected:isSelected(index),
              correct:isCorrect(index),
              incorrect:isIncorrect(index)
            }"
        >
          <p>{{answer | refactor}}</p>
        </div>
      </div>
      <button
        @click="onSubmit"
        :disabled="selectedItem === null || submitted"
      >
        Save
      </button>
      <button @click="onNext">
        Next
      </button>
    </div>
  </section>
</template>
<script>
  import lodash from 'lodash';

  export default {
    props: {
      currentQuestion: Object,
      onNext: Function,
      addPoints: Function
    },
    data() {
      return {
        selectedItem: null,
        shuffledAnswers: [],
        correctIndex: null,
        correctAnswer: false,
        submitted: false
      }
    },
    watch: {
      currentQuestion: {
        immediate: true,
        handler() {
          this.selectedItem = null;
          this.submitted = false;
          this.correctAnswer = false;
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
        if (!this.submitted) {
          this.selectedItem = index;
        }
      },
      onSubmit() {
        if (this.selectedItem === this.correctIndex) {
          this.correctAnswer = true;
        }
        this.submitted = true;
        this.addPoints(this.correctAnswer);
      },
      shuffleAnswers() {
        let answers = [
          ...this.currentQuestion.incorrect_answers,
           this.currentQuestion.correct_answer
         ];

         this.shuffledAnswers = lodash.shuffle(answers);
         this.correctIndex = this.shuffledAnswers.indexOf(this.currentQuestion.correct_answer);
      },
      isSelected(index) {
        return this.selectedItem === index ? true : false;
      },
      isCorrect(index) {
        if (this.correctIndex === index && this.submitted) {
          return true;
        }

        return false;
      },
      isIncorrect(index) {
        if (this.selectedItem === index && !this.correctAnswer && this.submitted) {
          return true;
        }

        return false;
      }
    },
    filters: {
      refactor(value) {
        if (!value) return ''
        value = value.toString()
        return unescape(value).replace(/&quot;/g, '"').replace(/&#039;/g, "'");
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

  .question-list.submitted {
    pointer-events: none;
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

  .incorrect {
    background-color: lightcoral;
  }

</style>
