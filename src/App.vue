<template>
  <div class="container">
    <div class="row">
        <div class="col-12">
          <div id="app">
            <div class="row">
              <div class="col-6">
              <Searchbox :savedStocks="savedStocks"/>
              </div>
              <div class="col-6">
                <Stocksbox :savedStocks="savedStocks" />
              </div>
            </div>
          </div>
        </div>
      </div>
  </div>
</template>

<script>
import Searchbox from './components/Searchbox.vue'
import Searchvalue from './components/Searchvalue.vue'
import Stocksbox from './components/Stocksbox.vue'

export default {
  name: 'app',
  components: {
    Searchbox,
    Searchvalue,
    Stocksbox
  },
  data: function() {
    return {
      savedStocks: []
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
