<template>
  <div class="recipes-show">
  	<div class="container">
  		<h2>{{ recipe.title }}</h2>
  		<h3>{{ recipe.ingredients }}</h3>
  		<h3>{{ recipe.directions }}</h3>
  		<h4>{{ recipe.prep_time }}</h4>

  		<router-link to="/">Back to index</router-link>
  	</div>
  </div>
</template>

<script>
import axios from "axios";
export default {
  data: function() {
    return {
      recipe: {}
    };
  },
  created: function() {
  	axios.get("http://localhost:3000/api/recipes/" + this.$route.params.id)
  	.then(response => {
  		this.recipe = response.data;
  	})
  },
  methods: {},
  computed: {}
};
</script>