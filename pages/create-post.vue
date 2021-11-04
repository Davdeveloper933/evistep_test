<template>
  <div>
  <h1>Create post</h1>
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
  <button @click="createPost">Create</button>
  </div>
</template>

<script>
export default {
  data () {
    return {
      title: null,
      body: null,
      userId: null
    }
  },
  methods: {
    createPost () {
      this.$axios.post('https://jsonplaceholder.typicode.com/posts',{
          title: this.title,
          body: this.body,
          userId: this.userId
        },
        {
          headers: {
            'Content-type': 'application/json; charset=UTF-8'
          }
        })
      .then(response => {
        alert('Post was created successfully')
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
