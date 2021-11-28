<template>
  <div class="home">
    <!-- src="https://cdnjs.cloudflare.com/ajax/libs/vue/2.5.15/vue.js"   -->
    <div v-for="cocktail in cocktails">
      <p>{{ cocktail.cocktail_name}}</p>
      <div id="app">
        <div class="pre-formatted">{{ cocktail.ingredient }}</div>
        </br>
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
    },
  };
</script>
