<template>
  <div class="container new">
    <form v-on:submit.prevent="createRecipe()">
      <h1>New Recipe</h1>
      <div class="form-group">
        Title:
        <input v-model="title" type="text" class="form-control" />
      </div>
      <div class="form-group">
        Chef:
        <input v-model="chef" type="text" class="form-control" />
      </div>
      <div class="form-group">
        Prep time:
        <input v-model="prepTime" type="text" class="form-control" />
      </div>
      <div class="form-group">
        Ingredients:
        <input v-model="ingredients" type="text" class="form-control" />
      </div>
      <div class="form-group">
        Directions:
        <input v-model="directions" type="text" class="form-control" />
      </div>
      <div class="form-group">
        Image url:
        <input v-model="imageUrl" type="text" class="form-control" />
      </div>
      <input type="submit" value="Create" class="btn btn-primary" />
    </form>
  </div>
</template>

<style></style>

<script>
import axios from "axios";

export default {
  data: function() {
    return {
      title: "",
      chef: "",
      prepTime: "",
      ingredients: "",
      directions: "",
      imageUrl: ""
    };
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
          this.$router.push("/recipes");
        })
        .catch(error => console.log(error.response));
    }
  }
};
</script>
