<template>
  <div class="col-sm-4">
    <div class="panel panel-info">
      <div class="panel-heading">
        <h3 class="panel-title">{{ stock.name }} <small>( Price: {{ stock.price }} | Quantity: {{ stock.quantity }} ) </small> </h3>
      </div>

      <div class="panel-body">
        <div class="pull-left">
          <input type="number" class="form-control" placeholder="Quantity" v-model="quantity" :class="{danger : insuffiecientQuantity}" />
        </div>
        <div class="pull-right">
          <button class="btn btn-success" @click="sellStock" :disabled="insuffiecientQuantity || quantity <= 0"> {{insuffiecientQuantity ? 'Not Enough Stocks' : 'Sell'}} </button>
        </div>
      </div>

    </div>
  </div>
</template>

<script>
import { mapActions } from 'vuex'

export default {
  props: ['stock'],
  data() {
    return {
      quantity: 0
    }
  },
  computed: {
    insuffiecientQuantity() {
      return this.quantity > this.stock.quantity
    }
  },
  methods: {
    ...mapActions({
      placeSellOrder: 'sellStock'
    }),
   sellStock() {
     const order = {
       stockId: this.stock.id,
       stockPrice: this.stock.price,
       quantity: this.quantity
     }
     this.placeSellOrder(order)
     this.quantity = 0
   }
   
  }
}
</script>

<style scoped>
.danger {
  border: 1px solid red;
}
</style>
