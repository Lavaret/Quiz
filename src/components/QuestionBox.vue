<template>
  <section class="question">
    <div class="question-wrap">
      <h2>Some question here?</h2>
      <div class="line"/>
      <div class="question-list">
        List of questions
      </div>
      <button>Save</button>
      <button>Next</button>
    </div>
  </section>
</template>

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

  .question-wrap {
    max-width: 50%;
    text-align: center;
    max-width: 50%;
  }

  .question {
    display: flex;
    justify-content: center;
  }

  .question-list {
    margin-top: 30px;
  }
</style>
