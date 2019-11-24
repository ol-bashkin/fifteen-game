<template>
  <div class="fifteen-game">
    <div class="fifteen-game__row">
      <SegmentCounter :data="{ title: 'ходы', value: moves.toString(), pattern: '88888'}" />
      <SegmentCounter :data="{ title: 'время', value: dateTime, pattern: '88:88'}" />
    </div>
    <FifteenTiles @move-tile="move" @shuffle="shuffle" />
  </div>
</template>

<script>
import SegmentCounter from '~/components/SegmentCounter.vue'
import FifteenTiles from '~/components/FifteenTiles.vue'
export default {
  components: {
    SegmentCounter,
    FifteenTiles
  },
  data () {
    return {
      started: false,
      moves: 0,
      time: 0,
      timer: null
    }
  },
  computed: {
    dateTime () {
      return new Date(this.time).toLocaleTimeString('ru-RU').slice(3)
    }
  },
  methods: {
    move () {
      this.moves += 1
      if (!this.started) {
        this.started = true
        this.setTimer()
      }
    },
    setTimer () {
      this.time = 0
      this.timer = setTimeout(this.tick, 1000)
    },
    tick () {
      this.time += 1000
      this.timer = setTimeout(this.tick, 1000)
    },
    shuffle () {
      clearTimeout(this.timer)
      this.timer = null
      this.moves = 0
      this.time = 0
      this.started = false
    }
  }
}
</script>

<style lang="scss" scoped>
@import '../assets/vars.scss';
.fifteen-game {
  box-sizing: border-box;
  display: flex;
  flex-direction: column;
  justify-content: flex-start;
  align-items: flex-start;
  width: 320px;
  padding: 20px;
  border-radius: 30px;
  background-color: $p-color-4;
  background-image: linear-gradient($p-color-4, $p-color-2);
  box-shadow: -10px -10px 30px 10px #fff, 10px 10px 30px 10px rgba($shadow-color, 0.4);
  &__row {
    display: flex;
    justify-content: flex-end;
    width: 100%;
    margin: 0 0 10px;
  }
}
</style>
