<template>
  <div class="container">
    <div id="app">
      <span>{{savedStocks}}</span>
      <Searchbox :savedStocks="savedStocks"/>
    </div>
  </div>
</template>

<script>
import Searchbox from './components/Searchbox.vue'
import Searchvalue from './components/Searchvalue.vue'

export default {
  name: 'app',
  components: {
    Searchbox,
    Searchvalue
  },
  data: function() {
    return {
      savedStocks: ["nir"]
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
