<template>
  <div class="posts-show">
    <h1>{{ post.title }}</h1>
    <img :src="post.image" :alt="post.title" />
    <p>{{ post.body }}</p>
    <router-link :to="`/posts/${post.id}/edit`">Edit</router-link>
    <button v-on:click="destroyPost()">Destroy</button>
    {{ destroySuccess }}
  </div>
</template>

<script>
import axios from "axios";
export default {
  data: function() {
    return {
      post: {},
      destroySuccess: "",
    };
  },
  created: function() {
    axios.get(`/api/posts/${this.$route.params.id}`).then(response => {
      this.post = response.data;
    });
  },
  methods: {
    destroyPost: function() {
      if (confirm("Are you sure you want to delete this post?")) {
        axios.delete(`/api/posts/${this.post.id}`).then(response => {
          console.log(response.data);
          this.destroySuccess = response.data.message;
          var self = this;
          setTimeout(function() {
            self.$router.push("/posts");
          }, 1500);
        });
      }
    },
  },
};
</script>
