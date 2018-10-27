<template>
  <div>
    <input type="text" class="form-control" v-on:keyup="keyup($event)" v-model="searchinput">
    <ul>
      <Searchvalue v-for="(item, index) in items" :key="index" :stock="item" :savedStocks="savedStocks"/>
    </ul>
  </div>
</template>

<script>
import Searchvalue from '../components/Searchvalue.vue'

export default {
  name: 'Searchbox',
  components: {
    Searchvalue
  },
  props: ['savedStocks'],
  data: function() {
    return {
      searchinput: "",
      t: null,
      spantext: "",
      items: [
      ]
    }
  },
  methods: {
    keyup: function (e) {
      clearTimeout(this.t);
      this.t = setTimeout(() => {
        fetch(`https://www.alphavantage.co/query?function=SYMBOL_SEARCH&keywords=${this.searchinput}&apikey=HJYURPR5Q6JKIFP5`)
        .then((response) => {
          return response.json();
        })
        .then((symbolsJson) => {
          this.items = [];
          symbolsJson = symbolsJson.bestMatches;
          symbolsJson.forEach((v,i)=> {
            this.items.push({"symbol":v["1. symbol"],"name":v["2. name"]});
          });
        });
      },1000);
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h3 {
  margin: 40px 0 0;
}
ul {
  list-style-type: none;
  padding: 1rem 0 1rem 0;
  margin-top: .5rem;
  border-radius: 0 0 1rem 1rem;
  border: 1px solid lightgray;
  background: whitesmoke;
}
a {
  color: #42b983;
}
</style>
