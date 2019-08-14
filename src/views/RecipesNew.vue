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
        <input type="file" v-on:change="setFile($event)" ref="fileInput" class="form-control" />
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
      image: ""
    };
  },
  methods: {
    setFile: function(event) {
      if (event.target.files.length > 0) {
        this.image = event.target.files[0];
      }
    },
    createRecipe: function() {
      console.log("Create the recipe...");
      var formData = new FormData();
      formData.append("title", this.title);
      formData.append("chef", this.chef);
      formData.append("prep_time", this.prepTime);
      formData.append("ingredients", this.ingredients);
      formData.append("directions", this.directions);
      formData.append("image_url", this.image);
      axios
        .post("/api/recipes", formData)
        .then(response => {
          console.log("Success", response.data);
          this.$router.push("/recipes");
        })
        .catch(error => console.log(error.response));
    }
  }
};
</script>
