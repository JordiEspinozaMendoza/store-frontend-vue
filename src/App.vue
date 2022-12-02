<script>
import "./styles.css";
import NavComponentVue from "./components/navbar";
export default {
  name: "App",
  components: {
    NavComponentVue
  },
  data() {
    return {
      message: "Hello World",
    };
  },
  methods: {},
  mounted() {},
};
</script>

<template>
  <div id="app">
    <NavComponentVue />
    <router-view />
  </div>
</template>

<style></style>
