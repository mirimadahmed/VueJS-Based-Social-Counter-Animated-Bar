<template>
  <div id="app">
    <img alt="Vue logo" src="./assets/logo.png">
    <Followers :data="demo_data" duration="1000" :animate="true"/>
  </div>
</template>

<script>
import Followers from './components/Followers.vue'

export default {
  name: 'app',
  components: {
    Followers
  },
  data() {
    return {
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
      ]
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
  color: #2c3e50;
  margin-top: 60px;
}
</style>
