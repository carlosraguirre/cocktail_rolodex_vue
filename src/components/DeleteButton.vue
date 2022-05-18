<template>
  <div>
    <button v-on:click="destroyCocktail(cocktail)">Delete Recipe</button>
  </div>  
</template>

<script>
  import axios from "axios";

  export default {
    // props: ["cocktails"],
    data: function () {
      return {

      };
    },
    methods: {     
      destroyCocktail: function(cocktail) {
        console.log(cocktail);
        axios.delete("/cocktails/" + cocktail.id).then((response) => {
          console.log(response.data);
          var index = this.cocktails.indexOf(cocktail);
          this.cocktails.splice(index, 1);
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