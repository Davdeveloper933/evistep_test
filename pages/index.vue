<template>
  <Posts :posts="posts"></Posts>
</template>

<script>
import Posts from "../components/Posts";
export default {
  components: {Posts},
  data() {
    return {
      posts: []
    }
  },
  mounted() {
    this.fetchPosts()
  },
  methods: {
    fetchPosts() {
      this.$axios.get('https://jsonplaceholder.typicode.com/posts')
      .then(response => {
        this.posts = response.data
      })
    }
  }
}
</script>
