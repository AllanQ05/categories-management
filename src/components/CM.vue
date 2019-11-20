<template>
  <div class="cm">
    <button v-on:click="load">load category</button>
    <div class="justify-content-between row">
      <nested-test class="column" v-model="store" />
      <raw-displayer class="column" :title="'Vuex Store'" :value="store" />
    </div>
  </div>
</template>

<script>
import NestedTest from "./nested/nested-test.vue";
import rawDisplayer from "./infra/raw-displayer.vue";

import Cookies from "universal-cookie";
export default {
  name: "CM",
  data() {
    return {
      search: [],
      store: []
    };
  },
  display: "Nested (v-model & vuex)",
  order: 16,
  components: {
    NestedTest,
    rawDisplayer
  },
  methods: {
    async load() {
      var axios = require("axios");
      var cookies = new Cookies();
      axios = axios.create({
        headers: { Authorization: cookies.get("token") }
      });
      var res = await axios
        .get("http://127.0.0.1:3000/api/v1/category")
        .then(res => {
          return res;
        });
      if (res.status == 200) {
        for (let indexData = 0; indexData < res.data.length; indexData++) {
          // res.data[indexData]._id = Date.now();
          if (res.data[indexData].children == null) {
            // res.data[indexData]._id = null;
            res.data[indexData].children = [];
          }
        }
        console.log(res.data);
        this.store = res.data;
      }
    }
  }
};
</script>

<style>
.column {
  flex: 50%;
}

/* Clear floats after the columns */
.row {
  display: flex;
}
</style>