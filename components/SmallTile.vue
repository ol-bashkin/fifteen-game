<template>
  <div class="small-tile">
    <slot />
  </div>
</template>

<style lang="scss" scoped>
@import '../assets/vars.scss';
.small-tile {
  margin: 10px;
  padding: 5px;
  border-radius: 10px;
  background-color: $p-color-3;
  box-shadow: -3px -3px 8px 2px #fff, 3px 3px 8px 2px rgba($shadow-color, 0.4);
}
</style>
