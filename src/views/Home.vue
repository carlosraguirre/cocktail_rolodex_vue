<template>
  <div class="home">
    <h1>{{ message }}</h1>
      <div v-for="cocktail in cocktails">
        <p>{{ cocktail.cocktail_name}}</p>
        <p>{{ cocktail.ingredient}}</p>
        <p>{{ cocktail.direction}}</p>
        <p>{{ cocktail.recipe_link}}</p>
        </br>
        <hr>
        </br>
      </div>
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
        axios.get("/cocktails").then((response) => {
          console.log(response.data);
          this.cocktails = response.data;
        });
      }
    },
  };
</script>
