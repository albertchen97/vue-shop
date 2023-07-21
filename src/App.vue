<template>
  <!-- <nav class="aligncenter">
    <router-link to="/">Home</router-link> |
    <router-link to="/checkout">Checkout</router-link>
  </nav> -->
  <nav-bar
    :cart="cart"
    :cartTotal="cartTotal"
    :cartQty="cartQty"
    @addItem="addItem"
    @deleteItem="deleteItem"
  />
  <div class="container">
    <router-view
      :cartTotal="cartTotal"
      :products="products"
      :cart="cart"
      @addItem="addItem"
      @deleteItem="deleteItem"
    />
  </div>
</template>

<script>
import NavBar from "@/components/NavBar";
export default {
  data: function () {
    return {
      cart: [],
      products: [],
    };
  },
  // Fetch products from API
  created() {
    fetch("https://hplussport.com/api/products/order/price")
      .then((response) => response.json())
      .then((data) => {
        this.products = data;
      });
  },
  components: {
    NavBar,
  },
  methods: {
    addItem(newProduct) {
      console.log(`Adding item:  ${newProduct.name} `);
      let existingProductIndex;
      let existingProduct = this.cart.filter(function (cartItem, index) {
        if (cartItem.product.id == Number(newProduct.id)) {
          console.log(`${newProduct.name} already exists at index ${index}`);
          existingProductIndex = index;
          return true;
        } else {
          console.log(`${newProduct.name} does not exist at index ${index}`);
          return false;
        }
      });

      if (existingProduct.length) {
        this.cart[existingProductIndex].qty++;
      } else {
        this.cart.push({ product: newProduct, qty: 1 });
      }
    },

    deleteItem(index) {
      console.log(`Deleting ${this.cart[index].product.name}`);
      if (this.cart[index].qty > 1) {
        this.cart[index].qty--;
      } else {
        this.cart.splice(index, 1);
      }
    },
  },
  computed: {
    cartTotal() {
      console.log("Calculating cartTotal");
      let total = 0;
      for (let itemIndex in this.cart) {
        total =
          total + this.cart[itemIndex].product.price * this.cart[itemIndex].qty;
      }
      console.log(`cartTotal = ${this.cartTotal}`);
      return total;
    },
    cartQty: function () {
      let qty = 0;
      for (let itemIndex in this.cart) {
        qty = qty + this.cart[itemIndex].qty;
      }
      return qty;
    },
  },
};
</script>

<style lang="scss">
$primary: #6f42c1;
@import "node_modules/bootstrap/scss/bootstrap";
</style>
