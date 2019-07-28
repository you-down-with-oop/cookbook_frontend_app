<template>
  <div class="home">
    <h1>New Recipe</h1>
    Title:
    <input v-model="title" type="text" />
    Chef:
    <input v-model="chef" type="text" />
    Prep time:
    <input v-model="prepTime" type="text" />
    Ingredients:
    <input v-model="ingredients" type="text" />
    Directions:
    <input v-model="directions" type="text" />
    Image url:
    <input v-model="imageUrl" type="text" />
    <button v-on:click="createRecipe()">Create</button>
    <h1>{{ message }}</h1>
    <div v-for="recipe in recipes">
      <h2>{{ recipe.title }}</h2>
      <img v-bind:src="recipe.image_url" alt="" />
      <p>Ingredients: {{ recipe.ingredients }}</p>
      <p>Directions: {{ recipe.directions }}</p>
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
      recipes: [],
      title: "",
      chef: "",
      prepTime: "",
      ingredients: "",
      directions: "",
      imageUrl: ""
    };
  },
  created: function() {
    axios.get("/api/recipes").then(response => {
      this.recipes = response.data;
      console.log(this.recipes);
    });
  },
  methods: {
    createRecipe: function() {
      console.log("Create the recipe...");
      var params = {
        title: this.title,
        chef: this.chef,
        prep_time: this.prepTime,
        ingredients: this.ingredients,
        directions: this.directions,
        image_url: this.imageUrl
      };
      axios
        .post("/api/recipes", params)
        .then(response => {
          console.log("Success", response.data);
          this.recipes.push(response.data);
          this.title = "";
          this.chef = "";
          this.prepTime = "";
          this.ingredients = "";
          this.directions = "";
          this.imageUrl = "";
        })
        .catch(error => console.log(error.response));
    }
  }
};
</script>
