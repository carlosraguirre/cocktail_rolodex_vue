<template>
  <div class="home">
    <h1>{{ message }}</h1>
  </div>
</template>

<style></style>

<script>
  import axios from "axios";
  export default {
    data: function () {
      return {
        message: "Welcome to Vue.js!",
        cocktails: []
      };
    },
    created: function () {
      this.cocktailsIndex();
    },
    methods: {
      cocktailsIndex: function () {
        console.log("in cocktails index");
        axios.get("http://localhost:3000/cocktails").then((response) => {
          console.log(response.data);
          this.cocktails = response.data;
        });
      }
    },
  };
</script>
