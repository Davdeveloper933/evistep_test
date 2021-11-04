<template>
  <div>
  <h1>Posts</h1>
    <div class="create-button">
      <nuxt-link class="btn" to="/create-post">Create post</nuxt-link>
    </div>

  <ul v-if="posts.length">
    <li v-for="post in posts">
      <div class="post-buttons__wrap">
        <nuxt-link :to="`/posts/${post.id}/see-comments`">See comments</nuxt-link>
        <nuxt-link :to="`/posts/${post.id}`">View</nuxt-link>
        <nuxt-link :to="`/posts/${post.id}/update`">Update</nuxt-link>
        <button @click="deletePost(post.id)">Delete</button>
      </div>
    </li>
  </ul>
  </div>
</template>

<script>
export default {
  name: "Posts",
  props:['posts'],
  data() {
    return {

    }
  },
  methods: {
    deletePost(id) {
      this.$axios.delete(`https://jsonplaceholder.typicode.com/posts/${id}`)
      .then(response => {
        alert('Post has been deleted successfully')
      })
    }
  }
}
</script>

<style scoped>
  .create-button {
    display: flex;
    justify-content: flex-end;
    padding-right: 40px;
  }
</style>
