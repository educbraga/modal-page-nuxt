<template>
  <div class="product-detail">
    <h1>{{ product.name }}</h1>
    <nuxt-link to="/featured">Back to Featured</nuxt-link>
  </div>
</template>

<script>
import products from "../../static/products";

export default {
  asyncData({ app, route }) {
    return {
      product: products.find(product => product.id === route.params.id)
    };
  }
};
</script>

<style scoped>
.product-detail {
  text-align: center;
}

.product-detail h1 {
  font-size: 36px;
  margin-bottom: 20px;
}
</style>
