<template>
  <section class="header">
    <div class="header">
      <p class="nav-element"><b>Fancy</b> quiz app</p>
      <p class="nav-element">Counter {{points}}/{{total}}</p>
    </div>
    <div class="line"></div>
  </section>
</template>
<script>

  export default {
    props: {
      points: Number,
      total: Number
    }
  }

</script>
<style type="scss" scoped>
  .header {
    display: flex;
    flex-wrap: wrap;
    margin-top: 30px;
  }

  .nav-element {
    margin-right: 15px;
    letter-spacing: 1px;
    font-size: 15px;
    margin-bottom: 10px;
    color: #6f7f94;
  }

</style>
