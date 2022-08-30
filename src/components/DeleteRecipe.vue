<template>
  <div>
    <button v-on:click="$emit('deleteCocktail')">Delete Recipe</button>
  </div>  
</template>

<script>
  import axios from "axios";

  export default {
    methods: {     
      destroyCocktail: function() {
        // console.log(cocktail);
        axios.delete("/cocktails/" + cocktail.id).then((response) => {
          // console.log(response.data);
          this.$emit('deleteCocktail', response.data);
        });
      }
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
</style>