<template>{{ dollar(amt) }}</template>

<script>
export default {
  name: "CurrencyItem",
  props: ["amt"],
  methods: {
    dollar(value) {
      return "$" + Number.parseFloat(value).toFixed(2);
    },
  },
  // created() {
  //   console.log(this.amt);
  // },
  // updated() {
  //   console.log(this.amt);
  // },
};
</script>

<style></style>
