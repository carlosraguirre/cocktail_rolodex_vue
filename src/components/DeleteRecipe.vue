<template>
  <div>
    <button v-on:click="destroyCocktail()">Delete Recipe</button>
  </div>  
</template>

<script>
  import axios from "axios";

  export default {
    emits: ['removeCocktail'],

    methods: {     
      destroyCocktail: function() {
        // console.log(cocktail);
        axios.delete("/cocktails/${cocktail.id}", cocktail).then((response) => {
          console.log(response.data);
          this.$emit('removeCocktail', response.data);
          // var index = this.cocktails.indexOf(cocktail);
          // this.cocktails.splice(index, 1);          
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