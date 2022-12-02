<script>
import "./styles.css";
const routes = [
  {
    label: "Home",
    path: "/",
  },
  {
    label: "Register",
    path: "/register",
  },
];
export default {
  name: "NavComponent",
  data() {
    return {
      routes,
    };
  },
};
</script>
<template>
  <div class="navbar__container">
    <div class="navbar__links">
      <router-link
        v-for="route in routes"
        :key="route.label"
        :to="route.path"
        class="navbar__link"
      >
        {{ route.label }}
      </router-link>
    </div>
  </div>
</template>
