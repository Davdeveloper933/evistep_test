<template>
<div v-if="post">
  <h2>{{post.title}}</h2>
  <div v-if="postComments">
    <div class="comment" v-for="comment in postComments">
      <span>name: {{comment.name}}</span>
      <span>email: {{comment.email}}</span>
      <span>{{comment.body}}</span>
    </div>
  </div>
</div>
</template>

<script>
export default {
  data() {
    return {
      post:null,
      postComments:null
    }
  },
  mounted() {
    this.fetchPost()
    this.fetchComments()
  },
  methods: {
    fetchComments () {
      this.$axios.get(`https://jsonplaceholder.typicode.com/posts/${this.$route.params.id}/comments`)
        .then(response => {
          this.postComments = response.data
        })
    },
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
  .comment {
    border: 1px solid;
    padding: 20px;
    margin: 10px 0;
    display: flex;
    flex-direction: column;
  }
</style>
