<template>
  <section class="question">
    <div class="question-wrap">
      <span class="category">{{currentQuestion.category}}</span>
      <h2>{{currentQuestion.question}}</h2>
      <div class="line"/>
      <div class="question-list">
        List of questions
      </div>
      <button>Save</button>
      <button @click="onNext">Next</button>
    </div>
  </section>
</template>
<script>
  export default {
    props: {
      currentQuestion: Object,
      onNext: Function
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
    max-width: 50%;
    text-align: center;
    max-width: 50%;
  }

  .question {
    padding: 15px;
    display: flex;
    justify-content: center;
  }

  .question-list {
    margin-top: 30px;
  }
</style>
