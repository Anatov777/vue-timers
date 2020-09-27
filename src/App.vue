<template>
  <div id="app">
    <div class="timers">
      <div><Timer /></div>
      <div v-for="timer in timers" :key="timer.index">
        <Timer />
      </div>
      <div class="add-timer" @click="addTimer"></div>
    </div>
  </div>
</template>

<script>
import Timer from "./components/Timer.vue";

export default {
  name: "App",
  components: {
    Timer,
  },
  data: () => ({
    timers: [],
  }),
  methods: {
    addTimer() {
      this.timers.push(this.timers.length+1);
    },
  },
};
</script>

<style lang="scss">
  @import "assets/index.scss";
</style>
