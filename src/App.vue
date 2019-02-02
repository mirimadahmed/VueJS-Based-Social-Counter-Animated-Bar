<template>
  <div id="app">
    <h1>Followers Component</h1>
    <Followers :data="demo_data" :duration="duration" :animate="animate"/>
    <br><br><br>
    <input type="button" @click="animate = true" value="Run Animation">
  </div>
</template>

<script>
import Followers from './components/Followers/Followers.vue'

export default {
  name: 'app',
  components: {
    Followers
  },
  data() {
    return {
      animate: false,
      demo_data: [
        {
          platform: 'youtube',
          followers: 110245,
        },
        {
          platform: 'instagram',
          followers: 455,
        },
        {
          platform: 'twitter',
          followers: 72400,
        },
      ],
      duration: 1000
    }
  }
}
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
}
</style>
