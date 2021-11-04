<template>
  <div v-if="post">
    <h1>{{ post.title}}</h1>
    <p>id: {{post.id }}</p>
    <p>body: <br> {{ post.body }}</p>
  </div>
</template>

<script>
export default {
  data() {
    return {
      post:null
    }
  },
  mounted() {
    this.fetchPost()
  },
  methods: {
    fetchPost () {
      this.$axios.get(`https://jsonplaceholder.typicode.com/posts/${this.$route.params.id}`)
        .then(response => {
          this.post = response.data
        })
    }
  }
}
</script>

<style scoped>

</style>
