<template>
  <div class="featured-products">
    <h1>Featured</h1>
    <ul>
      <li v-for="product in products" :key="product.id">
        <nuxt-link
          :to="{
            name: 'product-id',
            params: { id: product.id, slug: product.name.toLowerCase() }
          }"
        >{{ product.name }}</nuxt-link>
        <!-- THIS WOULD BE THE MODAL FOR THE PRODUCT -->
        <div v-if="activeModal === product.id">
          {{ product.name }}
          <button @click="hideProductModal">X</button>
        </div>
      </li>
    </ul>
  </div>
</template>

<script>
import products from "../../static/products";

export default {
  data() {
    return {
      activeModal: null
    };
  },
  asyncData() {
    return {
      products
    };
  },
  beforeRouteLeave(to, from, next) {
    if (to.name === "product-id") {
      this.displayProductModal(to);
    } else {
      next();
    }
  },
  methods: {
    displayProductModal(route) {
      this.activeModal = route.params.id;
      window.history.pushState({}, null, route.path);
    },
    hideProductModal() {
      this.activeModal = null;
      window.history.pushState({}, null, this.$route.path);
    }
  }
};
</script>

<style scoped>
.featured-products {
  text-align: center;
}

.featured-products h1 {
  font-size: 36px;
  margin-bottom: 40px;
}

.featured-products li {
  margin-bottom: 30px;
}

.featured-products a {
  font-size: 24px;
}

.featured-products button {
  background-color: #ddd;
  padding: 2px 10px;
}
</style>
