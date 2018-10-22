<template>
  <div class="home">
    <h1>All Recipes</h1>
    <div v-for="recipe in recipes">
      <h2>{{ recipe.title }}</h2>
      <h3>{{ recipe.ingredients }}</h3>
      <h3>{{ recipe.directions }}</h3>
      <router-link v-bind:to="'/recipes/' + recipe.id">More Info</router-link>
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
      recipes: []
    };
  },
  created: function() {
  	axios.get("http://localhost:3000/api/recipes").then(response => {
  		console.log(response.data);
      this.recipes = response.data
  	});
  },
  methods: {},
  computed: {}
};
</script>