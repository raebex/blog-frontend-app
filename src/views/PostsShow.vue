<template>
  <div class="posts-show">
    <h1>{{ post.title }}</h1>
    <img :src="post.image" :alt="post.title">
    <p>{{ post.body }}</p>
  </div>
</template>

<script>
import axios from "axios";
export default {
  data: function() {
    return {
      post: {},
    };
  },
  created: function() {
    axios.get(`/api/posts/${this.$route.params.id}`).then(response => {
      this.post = response.data;
    });
  },
};
</script>