<template>
<nav class="navbar navbar-expand-sm bg-dark navbar-dark">
  <!-- Brand -->
   <router-link to="/" class="navbar-brand">Stock Trader</router-link>

  <!-- Links -->
  <ul class="navbar-nav">
   <router-link to="/portfolio" activeClass="active" tag="li">
      <a class="nav-link">Portfolio</a>
    </router-link>
    <router-link to="stocks" activeClass="active" tag="li">
      <a class="nav-link">Stocks</a>
    </router-link>

  <strong class="navbar-text"> Funds: {{ funds | currency }} </strong>

    <li><a class="nav-link" @click="endDay">End Day</a></li>

    <!-- Dropdown -->
    <li class="nav-item dropdown">
      <a class="nav-link dropdown-toggle" href="#" id="navbardrop" data-toggle="dropdown">
         Save & Load
      </a>
      <div class="dropdown-menu">
        <a class="dropdown-item" href="#" @click="saveData">Save</a>
         <a class="dropdown-item" href="#" @click="loadData">Load</a>
      </div>
    </li>
  </ul>
</nav>
</template>

<script>
import { mapActions } from 'vuex'

export default {
  // data() {
  //   is
  // },
  computed: {
    funds() {
      return this.$store.getters.funds
    }
  },
  methods: {
    ...mapActions({
        randomizeStocks: 'randomizeStocks',
        fetchData: 'loadData'
    }),
    endDay() {
      this.randomizeStocks()
    },
    saveData() {
      const data = {
        funds: this.$store.getters.funds,
        stockPortfolio: this.$store.getters.stockPortfolio,
        stocks: this.$store.getters.stocks
      }
      this.$http.put('data.json', data)
    },
    loadData() {
      this.fetchData()
    }
  }
}
</script>

<style>

</style>
