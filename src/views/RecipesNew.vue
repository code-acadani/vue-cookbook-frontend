<template>
  <div class="recipes-new">
    <div class="container">
      <form v-on:submit.prevent="submit()">
        <h1>New Recipe</h1>
        <ul>
          <li class="text-danger" v-for="error in errors">{{ error }}</li>
        </ul>
        <div class="form-group">
          <label>Title:</label> 
          <input type="text" class="form-control" v-model="title">
        </div>
        <div class="form-group">
          <label>Ingredients:</label>
          <input type="text" class="form-control" v-model="ingredients">
        </div>
        <div class="form-group">
          <label>Directions:</label>
          <input type="text" class="form-control" v-model="directions">
        </div>
        <div class="form-group">
          <label>Image Url:</label>
          <input type="text" class="form-control" v-model="imageUrl">
        </div>
        <div class="form-group">
          <label>Prep Time:</label>
          <input type="number" class="form-control" v-model="prepTime">
        </div>
        <input type="submit" class="btn btn-primary" value="Submit">
      </form>
    </div>
  </div>
</template>

<script>
import axios from "axios";

export default {
  data: function() {
    return {
      title: "",
      ingredients: "",
      directions: "",
      imageUrl: "",
      prepTime: "",
      errors: []
    };
  },
  methods: {
    submit: function() {
      var params = {
        title: this.title,
        ingredients: this.ingredients,
        directions: this.directions,
        image_url: this.imageUrl,
        prep_time: this.prepTime
      };
      axios
        .post("http://localhost:3000/api/recipes", params)
        .then(response => {
          this.$router.push("/");
        })
        .catch(error => {
          this.errors = error.response.data.errors;
        });
    }
  }
};
</script>