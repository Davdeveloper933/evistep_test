<template>
  <div>
    <h1>Update post</h1>
    <div class="input_wrap">
      <label>
        <p>User id:</p>
        <input class="input" type="text" placeholder="Enter user ID" v-model="userId">
      </label>
      <label>
        <p>Title:</p>
        <input class="input" type="text" placeholder="Enter post title" v-model="title">
      </label>
      <label>
        <p>Body:</p>
        <textarea class="input" v-model="body" placeholder="Enter post body"></textarea>
      </label>
    </div>
    <button @click="savePost">Save</button>
  </div>
</template>

<script>
export default {
  data () {
    return {
      title: null,
      body: null,
      userId: null,
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
          this.title = this.post.title
          this.body = this.post.body
          this.userId = this.post.userId
        })
    },
    savePost () {
      this.$axios.put(`https://jsonplaceholder.typicode.com/posts/${this.$route.params.id}`,{
          id: this.userId,
          title: this.title,
          body: this.body,
          userId: this.userId,
        },
        {
          headers: {
            'Content-type': 'application/json; charset=UTF-8'
          }
        })
        .then(response => {
          alert('Post was updated successfully')
        })
        .catch(error => {
          alert('something went wrong')
        })
    }
  }
}
</script>

<style scoped>
.input_wrap {
  display: flex;
  flex-direction: column;
  width: 30%;
}
.input_wrap .input {
  width: 100%;
}
textarea {
  min-height: 150px;
}
</style>
