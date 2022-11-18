<template>
  <div id="app">
    <!-- Search Bar -->
    <!-- <div class="search-wrapper"> -->
      <!-- <input type="text" v-model="search" placeholder="Search.."/> -->

      <!-- <input type="text" v-model="search">
      <div v-for="cocktail in filteredCocktail" :key="cocktail.id">
        <cocktail :cocktail="cocktail"></cocktail>
      </div> -->

      <!-- <input class="form-control" type="text" placeholder="search cocktails">
      <button v-on:click="filter()">Search</button>
      <div v-for ="cocktail in filterCocktail">
        <h5>{{ cocktail.cocktail_name }}</h5>
      </div> -->

      
    <!-- </div> -->

    <!-- Add Recipe -->
    <div>
      <AddRecipe @addCocktail="addNewCocktail" />
    </div>
    </br>
    </br>
    <input type="text" v-model="search">

    <hr style="width:60%">

    <!-- Recipe Component -->
    <Recipe
      v-for="cocktail in cocktailCarlos"
      @removeCocktail=deleteCocktail
      @editRecipe=editCocktail
      :cocktail="cocktail" 
      :key="cocktail.id" 
    />
  </div>
</template>

<script>
  import axios from "axios";
  import Recipe from '@/components/Recipe.vue'
  import AddRecipe from '@/components/AddRecipe.vue'

  export default {
    components: {
      AddRecipe,
      Recipe
    },
    data: function () {
      return {
        cocktails: [],
        search: "",
      };
    },
    mounted: function () {
      this.cocktailsIndex();

    },
    computed: {
      cocktailCarlos() {
        return this.cocktails.filter(cocktail => 
          cocktail.ingredient.toLowerCase().includes(this.search.toLowerCase())
        );
      },
      filterCocktails() {
        return this.cocktails.filter(cocktail =>
          cocktail.ingredient.toLowerCase().includes(this.search.toLowerCase())
        );
      }
    },
    methods: {
      cocktailsIndex: function () {
        console.log("in cocktails index");
        axios.get("/cocktails").then((response) => {
          // console.log(response.data);
          this.cocktails = response.data;
        });
      },
      addNewCocktail: function (cocktail) {
        console.log("new cocktail", cocktail);
        this.cocktails = [
          cocktail, ...this.cocktails
            // spread operator
        ];
      },
      deleteCocktail: function (cocktailId) {
        console.log("delete cocktail", cocktailId);
        this.cocktails = this.cocktails.filter((cocktail) => cocktail.id !== cocktailId);
      },
      editCocktail: function (cocktail) {
        console.log("edit cocktail", cocktail);
      }
    },
  };
</script>

<style>
#original {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}
#nav {
  padding: 30px;
}
#nav a {
  font-weight: bold;
  color: #2c3e50;
}
#nav a.router-link-exact-active {
  color: #42b983;
}
.pre-formatted {
  white-space: pre;
}
.modal {
  width: 500px;
  margin: 0px auto;
  padding: 20px;
  background-color: #fff;
  border-radius: 7px;
  box-shadow: 0 2px 8px 3px;
  transition: all 0.2s ease-in;
  font-family: Helvetica, Arial, sans-serif;
}
.fadeIn-enter {
  opacity: 0;
}
.fadeIn-leave-active {
  opacity: 0;
  transition: all 0.2s step-end;
}
.fadeIn-enter .modal,
.fadeIn-leave-active.modal {
  transform: scale(1.1);
}
#container {
  text-align: center;
}
button {
  background-color: #04AA6D;
  border: none;
  color: white;
  padding: 10px;
  text-align: center;
  text-decoration: none;
  display: inline-block;
  font-size: 16px;
  margin: 4px 2px;
  border-radius: 10px;
}
.overlay {
  position: fixed;
  top: 0;
  left: 0;
  display: flex;
  justify-content: center;
  align-items: center;
  width: 100%;
  height: 100%;
  background: whitesmoke;
  z-index: 999;
  transition: opacity 0.2s ease;
}
</style>