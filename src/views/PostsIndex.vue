<template>
  <div class="posts-index">
    <h1>All Posts</h1>
    <div v-for="post in posts" :key="post.id">
      <h2>{{ post.title }}</h2>
      <router-link :to="`/posts/${post.id}`">
        <img :src="post.image" :alt="post.name" />
      </router-link>
      <p>{{ post.body }}</p>
      <p>Created {{ formattedTime(post.created_at) }}</p>
      <p v-if="$parent.getUserId() == post.user_id">Your post!</p>
    </div>
  </div>
</template>

<script>
import axios from "axios";
import moment from "moment";

export default {
  data: function() {
    return {
      posts: [],
    };
  },
  created: function() {
    axios.get("/api/posts").then(response => {
      this.posts = response.data;
    });
  },
  methods: {
    formattedTime: function(date) {
      return moment(date).fromNow();
    },
  },
};
</script>
