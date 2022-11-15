<template>
  <div>
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
  </div>
</template>

<script>
  import axios from "axios";

  export default {
    emits: ['editRecipe'],
    
    data: function () {
      return {
        editCocktailParams: {},
        isEditModalOpen: false,
      };
    },
    methods: {     
      updateCocktail: function() {
        console.log("updating Cocktail");
        axios.patch(`/cocktails/${this.editCocktailParams.id}`, this.editCocktailParams).then(response => {
          console.log(response.data);
          this.$emit('editRecipe', response.data);
          this.isEditModalOpen = !this.isEditModalOpen;
        });
      },
      editModalOpen: function (cocktail) {
        console.log(cocktail);
        this.editCocktailParams = cocktail
        this.isEditModalOpen = !this.isEditModalOpen;
      },
    },
  }
</script>

<style>
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
</style>