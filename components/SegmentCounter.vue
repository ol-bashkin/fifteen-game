<template>
  <div class="counter">
    <h3 class="counter__title">
      {{ data.title }}
    </h3>
    <SmallTile>
      <div class="counter__container">
        <p class="counter__pattern">
          {{ data.pattern }}
        </p>
        <p class="counter__value">
          {{ data.value }}
        </p>
      </div>
    </SmallTile>
  </div>
</template>

<script>
import SmallTile from '~/components/SmallTile.vue'

export default {
  components: {
    SmallTile
  },
  props: {
    data: {
      type: Object,
      required: true
    }
  }
}
</script>

<style lang="scss" scoped>
@import '../assets/vars';
@import '../assets/fonts';
.counter {
  &__title {
    margin: 10px 10px 0 0;
    font-size: 10px;
    text-transform: uppercase;
    font-weight: bold;
    text-align: right;
    letter-spacing: 1px;
  }
  &__container {
    position: relative;
    padding: 5px;
    border-radius: 5px;
    background-color: $s-color-3;
    background-image: linear-gradient(to right, $s-color-3, $s-color-4);
    border: 1px solid $s-color-1;
    color: $s-color-1;
    font-family: $Segment;
    font-size: 16px;
    text-align: right;
  }
  &__pattern  {
    opacity: 0.2;
  }
  &__value {
    position: absolute;
    top: 5px;
    right: 5px;
    width: 100%;
  }
}
</style>
