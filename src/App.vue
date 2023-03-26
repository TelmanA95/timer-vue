<template>
  <div id="app">
    <the-timer></the-timer>
    <the-timer  v-for="(timer, index) in timers" :key="index"></the-timer>
    <new-timer  @create-timer="addTimer"></new-timer>
  </div>
</template>

<script>
import TheTimer from './components/TheTimer/TheTimer.vue'
import NewTimer from './components/NewTimer/NewTimer.vue'

export default {
  name: 'App',
  components: {
    TheTimer,
    NewTimer
  },
  data() {
    return {
      timers: []
    }
  },
  methods: {
    addTimer(timer) {
      this.timers.push({ name: timer })
    }
  }
}

</script>

<style>
body{
  background: #353638FF;
}

#app{
  margin: 0 auto;
  max-width: 1200px;
  display: flex;
  flex-wrap: wrap;
  align-items: center;
  justify-content: center;
}

@media (max-width: 768px) {
  #app{
    max-width: 800px;
  }
  
}

</style>
