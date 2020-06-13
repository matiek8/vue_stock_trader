<template>
    <div>
        <div class="row mt-5">
            <app-stock v-for="stock in stocks" :stock="stock"></app-stock>
        </div>
    </div>
</template>

<script>
  import Stock from './Stock.vue'

  export default {
    name: "Stocks",
    components: {
      appStock: Stock,
    },
    computed: {
      stocks () {
        return this.$store.getters.stocks;
      }
    }
  }
</script>

<style scoped>

</style>
