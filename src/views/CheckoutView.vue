<template>
  <div class="container">
    <h1>Checkout</h1>

    <table class="table table-hover" v-if="cart.length">
      <caption class="text-right h3">
        <b>Total: </b>
        <currency-item :amt="Number(cartTotal)" />
      </caption>
      <thead>
        <tr>
          <th scope="col"></th>
          <th scope="col">Item</th>
          <th scope="col" class="text-center">Qty</th>
          <th scope="col" class="text-right">Price</th>
          <th scope="col" class="text-right">Sub-total</th>
        </tr>
      </thead>
      <tbody>
        <tr v-for="(item, index) in cart" :key="item.product.id">
          <td class="text-center">
            <div class="btn-group" role="group" aria-label="Basic example">
              <button
                class="btn btn-success"
                @click="this.$emit('addItem', item.product)"
              >
                +
              </button>
              <button
                class="btn btn-outline-success"
                @click="this.$emit('deleteItem', index)"
              >
                -
              </button>
            </div>
          </td>
          <th scope="row">{{ item.product.name }}</th>
          <td class="text-center">{{ item.qty }}</td>
          <td class="text-right">{{ item.product.price }}</td>
          <td class="text-right">
            <b>
              <currency-item :amt="item.qty * Number(item.product.price)" />
            </b>
          </td>
        </tr>
      </tbody>
    </table>
    <router-link class="btn btn-sm btn-success" to="/"
      >Keep Shopping</router-link
    >
  </div>
</template>

<script>
import CurrencyItem from "@/components/CurrencyItem.vue";
export default {
  name: "CheckoutView",
  props: ["cart", "cartTotal"],
  components: {
    CurrencyItem,
  },
  emits: ["addItem", "deleteItem"],
};
</script>

<style></style>
