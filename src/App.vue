<template>
  <div id="app">
    <h1>Timers</h1>
    <Timer />
  </div>
</template>

<script>
import Timer from './components/Timer.vue'

export default {
  name: 'App',
  components: {
    Timer
  }
}
</script>
