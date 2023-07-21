<template>
  <transition-group name="products" appear>
    <div
      v-for="item in filteredProducts"
      :key="item.id"
      id="item-list"
      class="row align-items-center"
    >
      <product-item :item="item" />
    </div>
  </transition-group>
</template>

<script>
import ProductItem from "@/components/ProductItem";
export default {
  name: "ProductList",
  props: ["filteredProducts"],
  components: {
    ProductItem,
  },
};
</script>

<style>
.products-enter-active,
.products-leave-active {
  transition: all 0.5s ease-in-out;
}
.products-enter-from {
  opacity: 0;
  transform: translateX(300px);
}
.products-leave-to {
  opacity: 0;
  transform: translateX(-300px);
}
</style>
