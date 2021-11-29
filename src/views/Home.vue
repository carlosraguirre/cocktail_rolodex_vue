<template>
  <div>  
    <div>
      <p>Add a Cocktail Recipe</p>
      <p><button v-on:click="cocktailCreate()">Add a cocktail recipe</button></p>
      <dialog id="cocktail-details">
        <form method="dialog">
          <p>Cocktail Name: <input type="text" v-model="newCocktailParams.cocktail_name"></p>
          <p>Cocktail Ingredients: <input type="text" v-model="newCocktailParams.ingredient"></p>
          <p>Cocktail Directions: <input type="text" v-model="newCocktailParams.direction"></p>
          <p>Link to Cocktail Recipe: <input type="text" v-model="newCocktailParams.recipe_link"></p>
          <p><button v-on:click="cocktailCreate()">Add a cocktail recipe</button></p>
          <p><button>Close</button></p>
        </form>
      </dialog>
    </div>
    <hr style="width:50%">
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
      <hr style="width:50%">
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
  import Modal from "@/components/Modal.vue";
  import axios from "axios";

  export default {
    // el: "#app",
    components: { 
      Modal
    },
    data: function () {
      return {
        cocktails: [],
        newCocktailParams: {},
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
      cocktailCreate: function () {
        console.log("create cocktail");
        var cocktailParams = {
          cocktail_name: this.newCocktailParams.cocktail_name,
          ingredient: this.newCocktailParams.ingredient,
          direction: this.newCocktailParams.direction,
          recipe_link: this.newCocktailParams.recipe_link,
        };
        axios.post("/cocktails", cocktailParams).then((response) => {
          console.log(response.data);
          this.cocktails.push(response.data);
          this.newCocktailParams = {};
          document.querySelector("#cocktail-details").showModal();
        });
      },     
    },
  };
</script>
