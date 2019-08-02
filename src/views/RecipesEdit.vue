<template>
  <div class="container home">
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
        this.$router.push("/recipes");
      });
    }
  }
};
</script>
