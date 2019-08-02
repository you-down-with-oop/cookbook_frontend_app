<template>
  <div class="container home">
    <h1>{{ message }}</h1>
    <div v-for="recipe in recipes">
      <h2>{{ recipe.title }}</h2>
      <img v-bind:src="recipe.image_url" alt="" />
      <router-link v-bind:to="`/recipes/${recipe.id}`">More info</router-link>
      <!-- <div>
        <button v-on:click="showRecipe(recipe)">More info</button>
      </div>
      <div v-if="recipe === currentRecipe">
        <p>Ingredients: {{ recipe.ingredients }}</p>
        <p>Directions: {{ recipe.directions }}</p>
        <p>Prep time: {{ recipe.prep_time }}</p>
        <h4>Edit recipe</h4>
        <div>
          Title:
          <input v-model="recipe.title" type="text" />
          Chef:
          <input v-model="recipe.chef" type="text" />
          Prep time:
          <input v-model="recipe.prep_time" type="text" />
          Ingredients:
          <input v-model="recipe.ingredients" type="text" />
          Directions:
          <input v-model="recipe.directions" type="text" />
          <button v-on:click="updateRecipe(recipe)">Update</button>
        </div>
        <button v-on:click="destroyRecipe(recipe)">Destroy recipe</button>
      </div> -->
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
    updateRecipe: function(inputRecipe) {
      var params = {
        title: inputRecipe.title,
        chef: inputRecipe.chef,
        prep_time: inputRecipe.prep_time,
        ingredients: inputRecipe.ingredients,
        directions: inputRecipe.directions
      };
      axios.patch("/api/recipes/" + inputRecipe.id, params).then(response => {
        console.log("Update successful", response.data);
        inputRecipe.title = response.data.title;
        inputRecipe.chef = response.data.chef;
        inputRecipe.prep_time = response.data.prep_time;
        inputRecipe.ingredients = response.data.ingredients;
        inputRecipe.directions = response.data.directions;
      });
    },
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
