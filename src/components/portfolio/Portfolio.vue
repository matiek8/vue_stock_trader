<template>
    <div>
        <div class="row mt-5">
            <app-stock v-for="stock in stocks"
                       :stock="stock"></app-stock>
        </div>
    </div>
</template>

<script>
  import Stock from "./Stock.vue";

  export default {
    name: "Portfolio",
    computed: {
      stocks () {
        return this.$store.getters.stockPortfolio;
      }
    },
    components: {
      appStock: Stock,
    }
  }
</script>

<style scoped>

</style>
