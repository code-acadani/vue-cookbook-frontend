<template>
  <div class="home">
    <div class="container">
    
      <h1>All Recipes</h1>
      <div v-for="recipe in recipes">
        <h2>{{ recipe.title }}</h2>
        <h4>Ingredients: {{ recipe.ingredients }}</h4>
        <h4>Directions: {{ recipe.directions }}</h4>
        <h4>Prep time: {{ recipe.prep_time }}</h4>
        <!-- <router-link v-bind:to="'/recipes/' + recipe.id">More Info</router-link> -->

        <!-- Button trigger modal -->
        <button type="button" class="btn btn-primary" data-toggle="modal" data-target="#exampleModal" v-on:click="setCurrentRecipe(recipe)">
          See More Info
        </button>

      </div>

      <!-- Modal -->
      <div class="modal fade" id="exampleModal" tabindex="-1" role="dialog" aria-labelledby="exampleModalLabel" aria-hidden="true">
        <div class="modal-dialog" role="document">
          <div class="modal-content">
            <div class="modal-header">
              <h5 class="modal-title" id="exampleModalLabel">{{ currentRecipe.title }}</h5>
              <button type="button" class="close" data-dismiss="modal" aria-label="Close">
                <span aria-hidden="true">&times;</span>
              </button>
            </div>
            <div class="modal-body">
              <p>{{ currentRecipe.ingredients }}</p>
              <p>{{ currentRecipe.directions }}</p>
              <img v-bind:src="currentRecipe.image_url" alt="">
            </div>
            <div class="modal-footer">
              <button type="button" class="btn btn-secondary" data-dismiss="modal">Close</button>
            </div>
          </div>
        </div>
      </div>
      <!-- End Modal -->
      
    </div>
  </div>
</template>

<style>
</style>

<script>
var axios = require('axios');
export default {
  data: function() {
    return {
      recipes: [],
      currentRecipe: {}
    };
  },
  created: function() {
  	axios.get("http://localhost:3000/api/recipes").then(response => {
  		console.log(response.data);
      this.recipes = response.data
  	});
  },
  methods: {
    setCurrentRecipe: function(recipe) {
      this.currentRecipe = recipe;
    }
  },
  computed: {}
};
</script>