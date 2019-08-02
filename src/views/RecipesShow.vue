<template>
  <div class="container show">
    <h2>{{ recipe.title }}</h2>
    <img v-bind:src="recipe.image_url" alt="" />
    <p>Ingredients: {{ recipe.ingredients }}</p>
    <p>Directions: {{ recipe.directions }}</p>
    <p>Prep time: {{ recipe.prep_time }}</p>
    <router-link v-bind:to="`/recipes/${recipe.id}/edit`">Edit recipe</router-link>
    <router-link to="/">Back to all recipes</router-link>
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
      recipe: {}
    };
  },
  created: function() {
    axios.get("/api/recipes/" + this.$route.params.id).then(response => {
      this.recipe = response.data;
    });
  },
  methods: {}
};
</script>
