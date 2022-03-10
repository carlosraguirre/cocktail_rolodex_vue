<template>
  <div id="app">
    <!-- Add Recipe -->
    <div>
      <transition name="modal">
        <div v-if="isOpen">
          <div class="overlay" v-on:click.self="isOpen = false;">
            <div class="modal">
              <h1>Add Cocktail</h1>
              <p><input type="text" v-model="newCocktailParams.cocktail_name" placeholder="Name"></p>
              <p><textarea v-model="newCocktailParams.ingredient" placeholder="Ingredients"></textarea></p>
              <p><textarea type="text" v-model="newCocktailParams.direction" placeholder="Directions"></textarea></p>
              <p><input type="text" v-model="newCocktailParams.recipe_link" placeholder="Link to Recipe"></p>
              <button v-on:click="cocktailCreate()">Add to rolodex</button>
            </div>
          </div>
        </div>
      </transition>
      <button v-on:click="isOpen = !isOpen;">
        {{ isOpen ? "Close" : "Add Cocktail Recipe" }}
      </button>
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
      <div>
        <button v-on:click="destroyCocktail(cocktail)">Delete Recipe</button>
      </div>
      <!-- Edit Recipe -->
      <!-- <div>
        <transition name="modal">
          <div v-if="isOpen">
            <div class="overlay" v-on:click.self="isOpen = false;">
              <div class="modal">
                <p><input type="text" v-model="editCocktailParams.cocktail_name" placeholder="Name"></p>
                <p><textarea v-model="editCocktailParams.ingredient" placeholder="Ingredients"></textarea></p>
                <p><textarea type="text" v-model="editCocktailParams.direction" placeholder="Directions"></textarea></p>
                <p><input type="text" v-model="editCocktailParams.recipe_link" placeholder="Link to Recipe"></p>
                <button v-on:click="updateCocktail()">Edit Recipe</button>
              </div>
            </div>
          </div>
        </transition>
        <button v-on:click="isOpen = !isOpen;">
          {{ isOpen ? "Close" : "Edit Recipe" }}
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

  export default {
    data: function () {
      return {
        cocktails: [],
        newCocktailParams: {},
        isOpen: false,
        // editCocktailParams: {},
        currentCocktail: {}
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
          // document.querySelector("#cocktail-details").showModal();
        });
        this.isOpen=false;
      },
      // updateCocktail: function() {
      //   console.log("updating Cocktail");
      //   axios.patch(`/cocktails/${this.params.id}`, this.editCocktailParams).then(response => {
      //     console.log(response.data);
      //     this.$router.push("/cocktails");
      //   });
      // },
      destroyCocktail: function(cocktail) {
        console.log(cocktail);
        axios.delete("/cocktails/" + cocktail.id).then((response) => {
          console.log(response.data);
          var index = this.cocktails.indexOf(cocktail);
          this.cocktails.splice(index, 1);
        });
      }
    },
  };
</script>

<style>
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
  background: #00000094;
  z-index: 999;
  transition: opacity 0.2s ease;
}
</style>