<template>
  <div class="token">
    <span>Authorization:</span>
    <button v-on:click="login">Get Now</button>
    <p style="white-space: pre-line;"></p>
    <br />
    <textarea v-model="token" placeholder="add token here"></textarea>
    <!-- <br /> -->
  </div>
</template>

<script>
import Cookies from "universal-cookie";
export default {
  name: "Token",
  data() {
    return {
      token: ""
    };
  },
  props: {},
  methods: {
    async login() {
      var axios = require("axios");
      // const Cookies = require("universal-cookie");
      const cookies = new Cookies();
      var res = await axios
        .post("http://127.0.0.1:3000/api/v1/auth", {
          grant_type: "password",
          username: "name01",
          password: "123456"
        })
        .then(function(res) {
          // console.log(res);
          if (res.status == 200) {
            // this.token = res.data.access_token;
            return res;
          }
        });
      // console.log(res);
      this.token = "Bearer " + res.data.access_token;
      // cookies.set("token", this.token);
      cookies.set("token", this.token, {});
    }
  }
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped></style>
