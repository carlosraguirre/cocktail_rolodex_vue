<template>
  <div id="app">
    <!-- Search Bar -->
    <!-- <div>
      <input class="form-control" type="text" v-model="filterValue" placeholder="search cocktails">
      <button v-on:click="filter()">Search</button>
      <div v-for ="cocktail in filterCocktails">
        <h5>{{ cocktail.cocktail_name }}</h5>
      </div>
    </div> -->

    <!-- Add Recipe -->
    <div>
      <AddRecipe @addCocktail="addNewCocktail" />
    </div>
    <hr style="width:60%">

    <!-- Cocktails Index -->
    <div v-for="cocktail in cocktails">
      <h2>{{ cocktail.cocktail_name}}</h2>
      <div id="original">
        <h4>Ingredients</h4>
        <div class="pre-formatted">{{ cocktail.ingredient }}</div>
        </br>
        <h4>Directions</h4>
        <div class="pre-formatted">{{ cocktail.direction }}</div>
        </br>
        <a v-bind:href="cocktail.recipe_link">Link to Recipe</a>
      </div>

      <!-- Delete Button -->
      <!-- <div>
        <button v-on:click="destroyCocktail(cocktail)">Delete Recipe</button>
      </div> -->
      <!-- Edit Recipe -->
      <!-- <div>
        <transition name="modal">
          <div v-if="isEditModalOpen">
            <div class="overlay" v-on:click.self="isEditModalOpen = false;">
              <div class="modal">
                <p><input type="text" v-model="editCocktailParams.cocktail_name" placeholder="Name"></p>
                <p><textarea v-model="editCocktailParams.ingredient" placeholder="Ingredients"></textarea></p>
                <p><textarea type="text" v-model="editCocktailParams.direction" placeholder="Directions"></textarea></p>
                <p><input type="text" v-model="editCocktailParams.recipe_link" placeholder="Link to Recipe"></p>
                <button v-on:click="updateCocktail()">Save changes</button>
              </div>
            </div>
          </div>
        </transition>
        <button v-on:click="editModalOpen(cocktail)">
          {{ isEditModalOpen ? "Close" : "Edit Recipe" }}
        </button>
      </div> -->
      </br>
      <hr style="width:60%">
      </br>
    </div>
  </div>
</template>

<script>
  import axios from "axios";
  import AddRecipe from '@/components/AddRecipe.vue'

  export default {
    components: {
      AddRecipe,
    },
    data: function () {
      return {
        cocktails: [],
        // editCocktailParams: {},
        // isEditModalOpen: false,
        // filterCocktails: {},
        // filterValue: ""
      };
    },
    mounted: function () {
      this.cocktailsIndex();
    //   // this.filter();
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
      // updateCocktail: function() {
      //   console.log("updating Cocktail");
      //   axios.patch(`/cocktails/${this.editCocktailParams.id}`, this.editCocktailParams).then(response => {
      //     console.log(response.data);
      //     this.isEditModalOpen = !this.isEditModalOpen;
      //   });
      // },
      // destroyCocktail: function(cocktail) {
      //   console.log(cocktail);
      //   axios.delete("/cocktails/" + cocktail.id).then((response) => {
      //     console.log(response.data);
      //     var index = this.cocktails.indexOf(cocktail);
      //     this.cocktails.splice(index, 1);
      //   });
      // },
      // editModalOpen: function (cocktail) {
      //   console.log(cocktail);
      //   this.editCocktailParams = cocktail
      //   this.isEditModalOpen = !this.isEditModalOpen;
      // },
      // filter: function () {
      //   console.log(this.filterValue)
      //   this.filterCocktails = []
      //   this.cocktails.forEach(cocktail => {
      //     if (cocktail.cocktail_name.includes(this.filterValue)) {
      //       this.filterCocktails.push(cocktail)
      //     }
      //   });
      // }
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
  border-radius: 10px
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