<template>
<div class="mt-5">
    <h1>Trade or View your Portfolio</h1>
    <h6>You may save & load your data</h6>
    <h6>Click on 'End Day' to begin a Ned Day</h6>
    <hr>
    <p>Your Funds: {{funds|currency}}</p>
</div>
</template>

<script>
  export default {
    name: "Home",
    computed: {
      funds () {
        return this.$store.getters.funds;
      }
    }
  }
</script>

<style scoped>

</style>
