<!-- eslint-disable vue/multi-word-component-names -->
<script>
import "./styles.css";
export default {
  data() {
    return {
      title: "Products page",
      getProducts: {
        loading: false,
        success: false,
        error: null,
        data: [],
      },
    };
  },
  // methods
  methods: {
    async handleGetProducts() {
      this.getProducts.loading = true;
      await fetch(`${process.env.VUE_APP_API_URL}/api/products`)
        .then((data) => data.json())
        .then((data) => {
          this.getProducts.data = data.products;
          this.getProducts.success = true;
          this.getProducts.loading = false;
        })
        .catch((error) => {
          this.getProducts.error = error;
          this.getProducts.loading = false;
        });
    },
  },
  // mounted hook
  mounted() {
    this.handleGetProducts();
  },
  // computed
  computed: {},
};
</script>
<template>
  <div class="home page__container">
    <div class="home__title">
      <h3>
        {{ title }}
      </h3>
    </div>
    <div class="loader" v-if="getProducts.loading">Loading products...</div>
    <div
      class="no__products"
      v-if="
        getProducts.success &&
        getProducts.data.length === 0 &&
        !getProducts.loading
      "
    >
      No products found
    </div>
    <div
      class="products__table"
      v-if="
        getProducts.success &&
        getProducts.data.length > 0 &&
        !getProducts.loading
      "
    >
      <table>
        <thead>
          <tr>
            <th>Product</th>
            <th>Price</th>
            <th>Quantity</th>
          </tr>
        </thead>
        <tbody>
          <tr v-for="product in getProducts.data" :key="product.id">
            <td>{{ product.name }}</td>
            <td>{{ product.price }}</td>
            <td>{{ product.quantity }}</td>
          </tr>
        </tbody>
      </table>
    </div>
  </div>
</template>
