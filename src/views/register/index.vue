<!-- eslint-disable vue/multi-word-component-names -->
<script>
import "./styles.css";
export default {
  name: "Register",
  data() {
    return {
      title: "Register page",
      formData: {
        name: "",
        price: "",
        quantity: 0,
      },
      registerProduct: {
        loading: false,
        success: false,
        error: null,
        data: [],
      },
    };
  },
  methods: {
    handleUpdateFormData(e) {
      const { name, value } = e.target;
      this.formData[name] = value;
    },
    async handleRegisterProduct(e) {
      e.preventDefault();
      this.registerProduct.loading = true;
      await fetch(`${process.env.VUE_APP_API_URL}/api/products`, {
        method: "POST",
        headers: {
          "Content-Type": "application/json",
        },
        body: JSON.stringify(this.formData),
      })
        .then((data) => data.json())
        .then((data) => {
          this.registerProduct.data = data.product;
          this.registerProduct.success = true;
          this.registerProduct.loading = false;
          this.formData = {
            name: "",
            price: "",
            quantity: 0,
          };
        })
        .catch((error) => {
          this.registerProduct.error = error;
          this.registerProduct.loading = false;
        });
    },
  },
  watch: {
    "registerProduct.success": function (val) {
      if (val === true) {
        this.$router.push("/");
      }
    },
  },
};
</script>
<template>
  <div class="register page__container">
    <div class="register__title">
      <h3>
        {{ title }}
      </h3>
    </div>
    <div class="form__container">
      <form @submit="handleRegisterProduct">
        <div class="form__group">
          <label for="name">Name</label>
          <input
            type="text"
            name="name"
            id="name"
            v-model="formData.name"
            @input="handleUpdateFormData"
          />
        </div>
        <div class="form__group">
          <label for="price">Price</label>
          <input
            type="number"
            name="price"
            id="price"
            v-model="formData.price"
            @input="handleUpdateFormData"
          />
        </div>
        <div class="form__group">
          <label for="quantity">Quantity</label>
          <input
            type="number"
            name="quantity"
            id="quantity"
            v-model="formData.quantity"
            @input="handleUpdateFormData"
          />
        </div>
        <div class="form__group">
          <button type="submit" :disabled="registerProduct.loading">
            {{ registerProduct.loading ? "Loading..." : "Register" }}
          </button>
        </div>
      </form>
    </div>
  </div>
</template>
