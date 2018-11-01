<template>
  <div>
    <input type="text" class="form-control" v-on:keyup="keyup($event)" v-model="searchinput">
    <ul v-show="!closed">
      <li class="close" v-on:click="closed=true">X</li>
      <li v-show="loading">Loading...</li>
      <li v-show="errorResults">Error showing results</li>
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
      loading: false,
      closed: true,
      searchinput: "",
      t: null,
      errorResults: false,
      spantext: "",
      items: [
      ]
    }
  },
  methods: {
    keyup: function (e) {
      if (this.searchinput=="") {
        this.closed = true;
        return false;
      }
      this.loading = true;
      this.closed = false;
      this.items = [];
      clearTimeout(this.t);
      this.t = setTimeout(() => {
        fetch(`https://www.alphavantage.co/query?function=SYMBOL_SEARCH&keywords=${this.searchinput}&apikey=HJYURPR5Q6JKIFP5`)
        .then((response) => {
          return response.json();
        })
        .then((symbolsJson) => {
          if (symbolsJson.hasOwnProperty("Note") ||
              symbolsJson.hasOwnProperty("Error Message")) errorResults=true;
          if (this.items.length>0) return false;
          this.loading = false;
          symbolsJson = symbolsJson.bestMatches;
          symbolsJson.forEach((v)=> {
            this.items.push({"symbol":v["1. symbol"],"name":v["2. name"]});
          });
        });
      },500);
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
  position: relative;
  list-style-type: none;
  padding: 1rem 0 1rem 0;
  margin-top: .5rem;
  border-radius: 0 0 1rem 1rem;
  border: 1px solid lightgray;
  background: whitesmoke;
}
li.close {
  position: absolute;
  top: .5rem;
  right: .5rem;
}
a {
  color: #42b983;
}
</style>
