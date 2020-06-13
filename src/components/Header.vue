<template>
    <nav class="navbar navbar-expand-lg navbar-light bg-light">
        <router-link class="navbar-brand"
                     to="/">Stock Trader
        </router-link>

        <div class="collapse navbar-collapse">
            <ul class="navbar-nav mr-auto">
                <router-link to="/portfolio"
                             class="nav-item"
                             tag="li"
                             active-class="active"><a class="nav-link">Portfolio</a></router-link>
                <router-link to="/stocks"
                             tag="li"
                             class="nav-item"
                             active-class="active"><a class="nav-link">Stocks</a></router-link>
            </ul>

            <ul class="navbar-nav my-2 my-lg-0">
                <li class="nav-item">
                    <a class="nav-link"
                       href="#"
                       @click="endDay">End Day</a>
                </li>
                <li class="nav-item dropdown">
                    <a class="nav-link dropdown-toggle"
                       role="button"
                       data-toggle="dropdown">
                        Save & Load
                    </a>
                    <div class="dropdown-menu"
                         aria-labelledby="navbarDropdown">
                        <a class="dropdown-item"
                           @click="saveData"
                           href="#">Save Data</a>
                        <a class="dropdown-item"
                           @click="loadData"
                           href="#">Load Data</a>
                    </div>
                </li>
                 <li class="nav-item">
                    <strong class="navbar-text">Funds: {{funds|currency}}</strong>
                </li>
            </ul>
        </div>
    </nav>
</template>

<script>
  export default {
    name: "Header",
    computed: {
      funds() {
        return this.$store.getters.funds;
      }
    },
    methods: {
      endDay() {
        this.$store.dispatch('randomizeStocks');
      },
      saveData() {
        const data = {
          funds: this.$store.getters.funds,
          stockPortfolio: this.$store.getters.stockPortfolio,
          stocks: this.$store.getters.stocks
        };
        this.$http.put('data.json', data)
      },
      loadData() {
        this.$store.dispatch('loadDataToStore');
      }
    }
  }
</script>

<style scoped>

</style>
