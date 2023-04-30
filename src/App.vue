<template>
  <HelloWorld msg="Welcome to Your Vue.js App"/>
  <CalculatorMain/>
</template>

<script>
import HelloWorld from './components/HelloWorld.vue'
import CalculatorMain from './components/CalculatorMain.vue'

export default {
  name: 'App',
  components: {
    HelloWorld,
    CalculatorMain
  }
}
</script>

<style>
body{
  overflow: hidden;
  margin: 0;
  padding: 0;
}
#app {
    display: flex;
    width: 100vw;
    height: 100vh;
    justify-content: center;
    align-items: center;
    background: rgb(9,38,121);
    background: linear-gradient(132deg, rgba(9,38,121,0.8911939775910365) 38%, rgba(0,116,255,1) 100%);
}
</style>
