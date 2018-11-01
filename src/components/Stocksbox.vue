<template>
    <ul class="list-group">
        <Stockitem  v-for="(item, index) in savedStocks" :key="index" :stock="item" />
    </ul>
</template>

<script>
import Stockitem from '@/components/Stockitem.vue'

export default {
  components: {
    Stockitem
  },
  name: 'Stocksbox',
  props: ['savedStocks'],
  data: function() {
    return {
      stocksInterval: null
    }
  },
  methods: {
  }
}
</script>

<style>

</style>
