<template>
  <div>
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
      <hr style="width:60%">
    </div>
    <DeleteRecipe />
    <EditRecipe />
  </div>  
</template>

<hr style="width:60%">

<script>
  import axios from "axios";
  import DeleteRecipe from '@/components/DeleteRecipe.vue'
  import EditRecipe from '@/components/EditRecipe.vue'

  export default {
    // props: ["cocktails"],
    components: {
      DeleteRecipe
    },  
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
  }
</script>

<style>
.pre-formatted {
  white-space: pre;
}
</style>