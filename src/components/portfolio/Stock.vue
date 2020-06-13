<template>
    <div class="col-sm-6 col-md-4">
        <div class="card  mb-3">
            <div class="card-header">
                <h3 class="card-title">
                    {{stock.name}}
                    <span class="card-text">Price: {{stock.price}} | Quantity: {{stock.quantity}}</span>
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
                                @click="sellStock"
                                :disabled="insufficientQuantity || quantity<=0">Sell
                        </button>
                    </div>
                </div>
                <p v-show="insufficientQuantity" class="text-danger"><small>Insufficient Quantity</small></p>
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
      insufficientQuantity() {
        return this.quantity > this.stock.quantity
      }
    },
    methods: {
      sellStock() {
        const order = {stockId: this.stock.id, stockPrice: this.stock.price, quantity: +this.quantity};
        this.$store.dispatch('sellStock', order);
        this.quantity = null
      },
    }
  }
</script>

<style scoped>

</style>
