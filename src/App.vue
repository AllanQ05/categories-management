<template>
  <div id="app">
    <img alt="Vue logo" src="./assets/logo.png" />
    <Token /><br />
    <CM />
    <!-- <button v-on:click="getCookie">Login</button> -->
  </div>
</template>

<script>
import Token from "./components/Token.vue";
import CM from "./components/CM.vue";
import Cookies from "universal-cookie";
export default {
  name: "app",
  components: {
    Token,
    CM
  },
  methods: {
    async getCookie() {
      // const cookie = require("universal-cookie");
      var cookies = new Cookies();
      console.log(cookies.get("token"));
    }
  }
};
</script>

<style></style>
