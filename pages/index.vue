<template>
  <div class="container">
    <h1 class="container__header">
      Пятнашки
    </h1>
    <FifteenGame />
  </div>
</template>

<script>
import FifteenGame from '~/components/FifteenGame.vue'

export default {
  components: {
    FifteenGame
  }
}
</script>

<style lang="scss">
@import "../assets/vars";
@import "../assets/fonts";

.container {
  display: flex;
  flex-direction: column;
  align-items: center;
  min-height: 100vh;
  padding: 40px;
  margin: 0 auto;
  color: $p-color-1;
  background-color: $p-color-3;
  text-align: center;
  font-family: $Gotham;

  &__header {
    font-size: 40px;
    margin: 0 0 40px;
  }
}

</style>
