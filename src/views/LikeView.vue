<template>
    <button @click="toggleLike">
      <span v-if="liked">Liked!</span>
      <span v-else>Like</span>
    </button>
  </template>
  
  <script>
  export default {
    data() {
      return {
        liked: false,
      };
    },
    methods: {
      toggleLike() {
        this.liked = !this.liked;
      },
    },
  };
  </script>
  
  <style scoped>
  button {
    /* Add your button styles here */
    padding: 5px 10px;
    border: 1px solid #ddd;
    border-radius: 3px;
    cursor: pointer;
  }
  </style>