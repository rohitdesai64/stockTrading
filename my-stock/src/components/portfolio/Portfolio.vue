<template>
  <div class="col-sm-12">
    <app-stock v-for="stock in stocks" :stock="stock" />
  </div>
</template>

<script>
import { mapGetters } from 'vuex'
import Stock from './Stock.vue'

export default {
  computed: {
    ...mapGetters({
      stocks: 'stockPortfolio'
    })
  },
  components: {
    appStock: Stock
  }
}
</script>

<style>

</style>
