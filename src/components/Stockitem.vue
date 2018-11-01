<template>
    <li class="list-group-item">{{stock.symbol}} ({{stock.name}}) - {{stock.value}} <span :class="{ up : isUp, down : !isUp}">{{type}}</span><span v-if="isLoading"> (L)</span></li>    
</template>

<script>
export default {
  name: 'Stockitem',
  props: ['stock'],
  data: function() {
    return {
      stockInterval: null,
      type: "",
      isUp: null,
      isLoading: true
    }
  },
  methods: {
  },
  mounted: function() {
    this.stockInterval = setInterval(() => {
        let old_value = this.stock.value;
        this.isLoading = true;
        fetch(`https://api.iextrading.com/1.0/stock/${this.stock.symbol.toLowerCase()}/batch?types=quote,news,chart&range=30s&last=10`)
            .then((response) => {
                return response.json();
            })
            .then((symbolJson) => {
                this.type = (parseFloat(symbolJson.quote.latestPrice) > parseFloat(this.stock.value)) ? "▲" : "▼";
                this.isUp = (parseFloat(symbolJson.quote.latestPrice) > parseFloat(this.stock.value)) ? true : false;
                this.stock.value = symbolJson.quote.latestPrice;
                this.isLoading = false;
                this.$forceUpdate();
        });
    },5000); 
  },
  destroy: function() {
      clearInterval(this.stockInterval);
  }
}
</script>

<style>
.up {
    color: green;
}
.down {
    color: red;
}
</style>
