<template>
  <div class="recipes-new">
    <form v-on:submit.prevent="createPost()">
      <h1>Create a Post</h1>
      <ul>
        <li class="text-danger" v-for="error in errors" v-bind:key="error">
          {{ error }}
        </li>
      </ul>
      <div class="form-group">
        <label>Title:</label>
        <input type="text" class="form-control" v-model="title">
      </div>
      <div class="form-group">
        <label>Body:</label>
        <input type="text" class="form-control" v-model="body">
      </div>
      <div class="form-group">
        <label>Image URL:</label>
        <input type="text" class="form-control" v-model="imageUrl">
      </div>
      <input type="submit" class="btn btn-primary" value="Create">
    </form>
  </div>
</template>

<script>
import axios from "axios";

export default {
  data: function() {
    return {
      title: "",
      body: "",
      imageUrl: "",
      errors: [],
    };
  },
  methods: {
    createPost: function() {
      var params = {
        title: this.title,
        body: this.body,
        image: this.imageUrl,
      };
      axios
        .post("/api/posts", params)
        .then(response => {
          console.log(response.data);
          this.$router.push("/posts");
        })
        .catch(error => {
          this.errors = error.response.data.errors;
        });
    }
  }
};
</script>