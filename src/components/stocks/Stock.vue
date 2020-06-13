<template>
    <div class="col-sm-6 col-md-4">
        <div class="card  mb-3">
            <div class="card-header">
                <h3 class="card-title">
                    {{stock.name}}
                    <span class="card-text">Price: {{stock.price}}</span>
                </h3>
            </div>
            <div class="card-body">
                <div class="form-row">
                    <div class="form-group col-md-9">
                        <input type="number"
                               class="form-control"
                               v-model="quantity"
                               placeholder="Quantity">
                    </div>
                    <div class="form-group col-md-3">
                        <button class="btn btn-success"
                                @click="buyStock"
                                :disabled="insufficientFunds || quantity<=0">Buy
                        </button>
                    </div>
                </div>
                <p v-show="insufficientFunds" class="text-danger"><small>Insufficient Funds</small></p>
            </div>
        </div>
    </div>
</template>

<script>
  export default {
    name: "Stock",
    props: ['stock'],
    data() {
      return {
        quantity: null,
      }
    },
    computed: {
      funds() {
        return this.$store.getters.funds;
      },
      insufficientFunds() {
        return this.quantity * this.stock.price > this.funds
      }
    },
    methods: {
      buyStock() {
        const order = {stockId: this.stock.id, stockPrice: this.stock.price, quantity: +this.quantity};
        this.$store.dispatch('buyStock', order);
        this.quantity = null
      },
    }
  }
</script>

<style>
    span.card-text {
        font-size: 14px;
    }
</style>
