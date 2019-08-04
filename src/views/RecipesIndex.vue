<template>
  <div class="container home">
    <div class="row">
      <div v-for="recipe in recipes" class="col-sm-4">
        <div class="card">
          <img v-bind:src="recipe.image_url" class="card-img-top" alt="..." />
          <div class="card-body">
            <h2 class="card-title">{{ recipe.title }}</h2>
            <p>by {{ recipe.chef }}</p>
            <router-link v-bind:to="`/recipes/${recipe.id}`">More info</router-link>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<style>
img {
  width: 100%;
}
.card {
  margin-bottom: 2rem;
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
  methods: {}
};
</script>
