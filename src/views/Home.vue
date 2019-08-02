<template>
  <div class="container home">
    <h1>{{ message }}</h1>
    <div v-for="recipe in recipes">
      <h2>{{ recipe.title }}</h2>
      <img v-bind:src="recipe.image_url" alt="" />
      <router-link v-bind:to="`/recipes/${recipe.id}`">More info</router-link>
    </div>
  </div>
</template>

<style>
img {
  width: 100%;
}
</style>

<script>
import axios from "axios";

export default {
  data: function() {
    return {
      message: "Welcome to Vue.js!",
      recipes: []
    };
  },
  created: function() {
    axios.get("/api/recipes").then(response => {
      this.recipes = response.data;
      console.log(this.recipes);
    });
  },
  methods: {
    destroyRecipe: function(inputRecipe) {
      axios.delete("/api/recipes/" + inputRecipe.id).then(response => {
        console.log("Delete successful", response.data);
        var index = this.recipes.indexOf(inputRecipe);
        this.recipes.splice(index, 1);
      });
    }
  }
};
</script>
