<template>
<div>
  <h1>Traide or View your Portfolio</h1>
  <h6>You may save & Load Data</h6>
  <h6>Click on 'End Day' to start new Day!</h6>
  <hr>
  <p> Your Funds : {{ funds | currency }} </p>

</div>
</template>

<script>
export default {
  computed: {
    funds() {
      return this.$store.getters.funds
    }
  }
}
</script>

<style>

</style>
