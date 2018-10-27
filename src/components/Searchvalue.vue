<template>
    <li v-on:click="saveStock(stock)">{{ stock.symbol }} ( {{stock.name}} )</li>
</template>

<script>
export default {
  name: 'Searchvalue',
  props: ['stock','savedStocks'],
  data: function() {
    return {
    }
  },
  methods: {
      saveStock: function (stock) {
          this.savedStocks.push(stock);
      }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>

li {
    width: inherit;
    padding: .5rem 0 .5rem 1rem;
    text-align: left;
}

li:hover {
    background: yellow;
    cursor: pointer;
}

</style>
