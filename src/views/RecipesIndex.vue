<template>
  <div class="container home">
    <div>
      <button v-on:click="sortAttribute = 'title'" class="btn btn-primary">Sort by title</button>
      <button v-on:click="sortAttribute = 'prep_time'" class="btn btn-primary">Sort by prep time</button>
    </div>
    <br />
    Search:
    <input v-model="searchFilter" type="text" list="titles" />
    <datalist id="titles">
      <option v-for="recipe in recipes">{{ recipe.title }}</option>
    </datalist>
    <transition-group class="row" appear enter-active-class="animated zoomInDown" leave-active-class="animated fadeOut">
      <div
        v-for="recipe in orderBy(filterBy(recipes, searchFilter, 'title'), sortAttribute)"
        v-bind:key="recipe.id"
        class="col-sm-4"
      >
        <div class="card" v-bind:class="{ selected: recipe === currentRecipe }" v-on:click="currentRecipe = recipe">
          <img v-bind:src="recipe.image_url" class="card-img-top" alt="..." />
          <div class="card-body">
            <h2 class="card-title">{{ recipe.title }}</h2>
            <p>by {{ recipe.chef }}</p>
            <p>Prep time: {{ recipe.prep_time }}</p>
            <router-link v-bind:to="`/recipes/${recipe.id}`">More info</router-link>
          </div>
        </div>
      </div>
    </transition-group>
  </div>
</template>

<style>
img {
  width: 100%;
}
.card {
  margin-bottom: 2rem;
}
.selected {
  color: white;
  background-color: steelBlue;
  transition: background-color 1s ease;
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
      searchFilter: "",
      sortAttribute: "title",
      currentRecipe: {}
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
