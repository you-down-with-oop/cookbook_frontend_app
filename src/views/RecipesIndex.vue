<template>
  <div class="container home">
    Search:
    <input v-model="searchFilter" type="text" list="titles" />
    <datalist id="titles">
      <option v-for="recipe in recipes">{{ recipe.title }}</option>
    </datalist>
    <div class="row">
      <div v-for="recipe in filterBy(recipes, searchFilter, 'title', 'chef')" class="col-sm-4">
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
import Vue2Filters from "vue2-filters";

export default {
  mixins: [Vue2Filters.mixin],
  data: function() {
    return {
      message: "Welcome to Vue.js!",
      recipes: [],
      searchFilter: ""
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
