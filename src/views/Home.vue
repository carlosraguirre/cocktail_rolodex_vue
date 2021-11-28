<template>
  <div class="home">
    <!-- src="https://cdnjs.cloudflare.com/ajax/libs/vue/2.5.15/vue.js"   -->
    <div v-for="cocktail in cocktails">
      <h2>{{ cocktail.cocktail_name}}</h2>
      <div id="app">
        <h4>Ingredients</h4>
        <div class="pre-formatted">{{ cocktail.ingredient }}</div>
        </br>
        <h4>Directions</h4>
        <div class="pre-formatted">{{ cocktail.direction }}</div>
        <a v-bind:href="cocktail.recipe_link">Link to Recipe</a>
      </div>        
      </br>
      <hr>
      </br>
    </div>
  </div>
</template>

<style>
.pre-formatted {
  white-space: pre;
}
</style>

<script>
  import axios from "axios";
  export default {
    // el: "#app",
    data: function () {
      return {
        cocktails: [],
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
      },
    },
  };
</script>
