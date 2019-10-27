<template>
  <section class="finish">
    <h2>Finish!</h2>
    <button @click="startGame">Start again</button>
  </section>
</template>
<script>
  export default {
    props: {
      getQuestions: Function
    },
    methods: {
      startGame() {
        location.reload();
      }
    }
  }
</script>

<style type="css" scoped>
  .finish {
    text-align: center;
    margin-top: 50px;
  }

  button {
    width: 150px;
    height: 50px;
  }
</style>
