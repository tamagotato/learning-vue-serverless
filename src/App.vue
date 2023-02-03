<template>
  <div id="app">
    <img alt="Vue logo" src="./assets/logo.png" />
    <br />
    Value 1:
    <input id="frmval1" type="text" placeholder="value_1" />
    <br />
    Value 2:
    <input id="frmval2" type="text" placeholder="Value_2" />
    <br />

    <label>This info is processed on Lambda</label>
    <b>
      <h2 id="answerhere"></h2>
    </b>
    <br />

    <button v-on:click="loadData">Compute</button>

    <HelloWorld msg="Welcome to Your Vue.js App" />
  </div>
</template>

<script>
import HelloWorld from "./components/HelloWorld.vue";
import axios from "axios";

export default {
  name: "App",
  components: {
    HelloWorld,
  },
  methods: {
    loadData: function () {
      console.log("Try and get Lambda Response");
      var value1 = 0;

      if (!document.getElementById("frmval1").value) {
        value1 = 0;
      } else value1 = document.getElementById("frmval1").value.toString();

      var value2 = 0;

      if (!document.getElementById("frmval2").value) {
        value2 = 0;
      } else value2 = document.getElementById("frmval2").value.toString();

      console.log(
        "Try and get Lambda Response. we will send val 1 and val 2 for processing in lambda"
      );

      console.log(
        "value 1 is " +
          value1.toString() +
          " and value 2 is " +
          value2.toString()
      );

      let config = {
        headers: { header1: value1, header2: value2 },
      };

      let data = {
        HTTP_CONTENT_LANGUAGE: self.language,
      };

      let url =
        "https://upq4sdk6d2.execute-api.us-east-2.amazonaws.com/default/vue-test";

      axios.post(url, data, config).then(
        (response) => {
          document.getElementById("answerhere").innerHTML = "The sum of val 1 and val 2 is " + response.data.toString()
          console.log(response.data.toString());
        },
        (response) => {
          console.log(response);
        }
      );
    },
  },
  data() {
    return {
      text: "",
    };
  },
};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
