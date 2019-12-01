<template>
  <div id="app">    
       <ShopIt/>
  </div>
</template>

<script>

import ShopIt from '@/components/ShopIt.vue'
export default {
  name: 'app',
  components: {
    ShopIt
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
 
}
</style>
