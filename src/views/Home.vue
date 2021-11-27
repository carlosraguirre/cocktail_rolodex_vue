<template>
  <div class="home">
    <h1>{{ message }}</h1>
      <div v-for="cocktail in cocktails">
        <p>{{ cocktail.cocktail_name}}</p>
        <ul style="list-style: none;">
          <li>{{ cocktail.ingredient }}</li>
          <li>{{ cocktail.direction }}</li>
          <a v-bind:href="cocktail.recipe_link">Link to Recipe</a>
        </ul>
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
        cocktails: [],
        // splitedStrings: "",
      };
    },
    created: function () {
      this.cocktailsIndex();
      // this.stringSplit();
    },
    methods: {
      cocktailsIndex: function () {
        console.log("in cocktails index");
        axios.get("/cocktails").then((response) => {
          console.log(response.data);
          this.cocktails = response.data;
        });
      },
      // stringSplit: function () {
      //   this.splitedStrings = this.cocktails.split("\n")
      // }
    },
  };
</script>
