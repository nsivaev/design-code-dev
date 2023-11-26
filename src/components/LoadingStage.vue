<script setup>

</script>

<template>
    <div class="wrapper">
        <h1>ПОДОЖДИТЕ, ВАШ ЗАПРОС ОБРАБАТЫВАЕТСЯ...</h1>
        <div class="loading-background"></div>
    </div>
</template>

<style scoped>

  .wrapper h1 {
      font-family: 'Montserrat', sans-serif;
      font-weight: bold;
      text-align: left;
      font-size: 30px;
      padding-top: 48px;
  }

  .loading-background {
      background-image: url(src/components/background/loading-background.jpg);
      background-position: right;
      background-repeat: no-repeat;
      background-size: cover;
      width: 100vw;
      height: 100vh;
      position: relative;
  }
</style>
