<template>
  <section class="container">
    <range-selector v-model.number="max" :filteredProducts="filteredProducts" />
    <product-list :filteredProducts="filteredProducts" />
  </section>
</template>

<script>
import ProductList from "@/components/ProductList.vue";
import RangeSelector from "@/components/RangeSelector.vue";

export default {
  name: "HomeView",
  data: function () {
    return {
      max: 50,
      cart: [],
      displayCart: false,
    };
  },
  props: ["products"],
  components: {
    ProductList,
    RangeSelector,
  },
  computed: {
    filteredProducts() {
      return this.products.filter((item) => item.price < this.max);
    },
  },
};
</script>
