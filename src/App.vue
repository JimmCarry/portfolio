<template>
  <div id="nav">
    <router-link to="/">Home</router-link>
    <router-link to="/about">About</router-link>
    <router-link to="/portfolio">Portfolio</router-link>
    <router-link to="/contact">Contact</router-link>
  </div>
  <router-view />
  <FollowIconsBar />
  
</template>

<script>
import { reactive, toRefs } from 'vue'
import FollowIconsBar from './components/FollowIconsBar'

export default {
  components: {
    FollowIconsBar
  },
    setup () {
        const state = reactive({
            count: 0,
        })
    
        return {
            ...toRefs(state),
        }
    }
}
</script>

<style lang="scss">
body {
  background-color: #2a2a2a;
  margin: 0;
  width: 100%;
  height: 100%;
  font-size: 14px;
  font-family: 'Roboto Mono', monospace;
}
a {
  text-decoration: none;
}
#app {
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #fff;
  max-width: 1200px;
  height: 600px;
  margin: 0 auto;
  position: relative;
  display: flex;
  flex-direction: column;
  justify-content: center;
  //background-color: #bada55;
}
#nav {
  padding: 2rem;
  .router-link-active {
    color: #fff;
  }
  a {
    color: grey;
    padding-right: 1rem;
  }
}
</style>
