<template>
  <div>
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
    </br>
    <!-- Delete Button -->
    <div>
      <!-- <DeleteRecipe @removeCocktail="deleteCocktail(cocktail)" /> -->
      <button v-on:click="destroyCocktail()">Delete Recipe</button>
    </div>

    <!-- Edit Recipe -->
    <div>
      <!-- <EditRecipe @editRecipe="editCocktail" /> -->
    </div>
    </br>
    <hr style="width:60%">
    </br>
  </div>
</template>

<script>
  import axios from "axios";
  import DeleteRecipe from '@/components/DeleteRecipe.vue';
  import EditRecipe from '@/components/EditRecipe.vue';

  export default {
      // components: {
      //     DeleteRecipe,
      //     EditRecipe,
      //   },
      emits: ['removeCocktail'],
      props: {cocktail:{type: Object, required: true}}, 

      methods: {     
        destroyCocktail: function() {
          axios.delete(`/cocktails/${this.cocktail.id}`).then((response) => {
            console.log(this.cocktail.id);
            this.$emit('removeCocktail', this.cocktail.id);
            // var index = this.cocktails.indexOf(cocktail);
            // this.cocktails.splice(index, 1);          
          });
        }
      },
    }

</script>

