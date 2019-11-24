<template>
  <div class="fifteen">
    <ul class="fifteen__container">
      <li v-if="isWin" class="fifteen__win">
        Победа!
      </li>
      <li
        v-for="(tile, index) in tiles"
        v-if="tile !== 0"
        :key="tile"
        @click="move($event, index)"
        :class="`fifteen__tile--${order[index]}`"
        class="fifteen__tile"
      >
        {{ tile }}
      </li>
    </ul>
    <button @click="shuffle" class="fifteen__button">
      Перемешать
    </button>
  </div>
</template>

<script>
export default {
  data () {
    return {
      tiles: [1, 2, 3, 4, 5, 6, 7, 8, 9, 10, 11, 12, 13, 14, 15, 0],
      order: [0, 1, 2, 3, 4, 5, 6, 7, 8, 9, 10, 11, 12, 13, 14],
      hole: 15
    }
  },
  computed: {
    isWin () {
      return !this.order.some((item, index) => { return item !== index })
    }
  },
  mounted () {
    this.shuffle()
  },
  methods: {
    move (event, index) {
      const newTileIndex = this.order[index]
      const newHoleIndex = this.order[this.hole]
      if (newHoleIndex - newTileIndex === 4 || newTileIndex - newHoleIndex === 4 ||
         (newHoleIndex - newTileIndex === 1 && newHoleIndex % 4 !== 0) ||
         (newTileIndex - newHoleIndex === 1 && newTileIndex % 4 !== 0)) {
        this.swap(this.hole, index)
        this.$emit('move-tile')
      }
    },
    swap (i1, i2) {
      const tempItem = this.order[i1]
      this.order.splice(i1, 1, this.order[i2])
      this.order.splice(i2, 1, tempItem)
    },
    shuffle () {
      const newArray = this.order.filter(item => item !== this.hole)
      for (let i = newArray.length - 1; i > 0; i--) {
        const j = Math.floor(Math.random() * (i + 1));
        [newArray[i], newArray[j]] =
        [newArray[j], newArray[i]]
      }
      newArray.push(this.hole)
      this.order = newArray
      if (this.isntSolvable(this.order)) {
        this.swap(0, 1)
      }
      this.$emit('shuffle')
    },
    isntSolvable (arr) {
      let disorderCount = 0
      for (let i = 1, length = arr.length - 1; i < length; i++) {
        for (let j = i - 1; j >= 0; j--) {
          if (arr[j] > arr[i]) { disorderCount++ }
        }
      }
      return (disorderCount % 2)
    }
  }
}
</script>

<style lang="scss" scoped>
@import "../assets/vars";
.fifteen {
  &__container {
    position: relative;
    display: flex;
    flex-wrap: wrap;
    width: 280px;
    height: 280px;
    margin: 0 0 10px;
    align-items: flex-start;
    justify-content: flex-start;
    padding: 0;
    list-style-type: none;
  }
  &__tile {
    position: absolute;
    width: 50px;
    height: 50px;
    margin: 10px;
    border-radius: 10px;
    background-color: $p-color-2;
    box-shadow: -3px -3px 8px 2px #fff, 3px 3px 8px 2px rgba($shadow-color, 0.4);
    font-size: 24px;
    line-height: 50px;
    text-align: center;
    font-weight: bold;
    transition: transform 0.2s ease-in-out;
    cursor: pointer;
    &--0  { transform: translate(0,     0) }
    &--1  { transform: translate(70px,  0) }
    &--2  { transform: translate(140px, 0) }
    &--3  { transform: translate(210px, 0) }
    &--4  { transform: translate(0,     70px) }
    &--5  { transform: translate(70px,  70px) }
    &--6  { transform: translate(140px, 70px) }
    &--7  { transform: translate(210px, 70px) }
    &--8  { transform: translate(0,     140px) }
    &--9  { transform: translate(70px,  140px) }
    &--10 { transform: translate(140px, 140px) }
    &--11 { transform: translate(210px, 140px) }
    &--12 { transform: translate(0,     210px) }
    &--13 { transform: translate(70px,  210px) }
    &--14 { transform: translate(140px, 210px) }
    &--15 { transform: translate(210px, 210px) }
  }
  &__win {
    position: absolute;
    z-index: 2;
    top: 0;
    right: 0;
    bottom: 0;
    left: 0;
    display: flex;
    justify-content: center;
    align-items: center;
    font-size: 24px;
    font-weight: bold;
    background-color: rgba($p-color-3, 0.6);
    backdrop-filter: blur(4px);
  }
  &__button {
    width: 260px;
    height: 50px;
    padding: 0;
    margin: 10px;
    border: none;
    background-color: $p-color-2;
    box-shadow: -3px -3px 8px 2px #fff, 3px 3px 8px 2px rgba($shadow-color, 0.4);
    border-radius: 10px;
    color: $p-color-1;
    font-family: inherit;
    font-weight: bold;
    font-size: 16px;
    line-height: 50px;
    cursor: pointer;
    &:focus {
      outline: none;
    }
  }
}
</style>
