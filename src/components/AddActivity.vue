<template>
  <div id="add">
    
    <h2>Add New Activity</h2>
    <p class="error" v-show="error" v-for="error in errors" v-bind:key="error">
      {{ error }}
    </p>

    <div>
      <label for="title">Title </label>
      <input id="title" v-model="title">
    </div>
  
    <div>
      <label for="youtube-url">YouTube URL</label>
      <input id="youtube-irl" v-model="url">
    </div>

    <button v-on:click="add">Add</button>
 
  </div>
</template>

<script>

export default {
  name: 'AddActivity',
  data() { 
    return  {
      title: '',
      url: '',
      errors: []
    }
  },
  methods: {
    add() {
      this.errors = []

      if (!this.title) {
        this.errors.push('Enter a title')
      }

      // Example video URL is https://www.youtube.com/watch?v=aAxGTnVNJiE
      // Notice the ID at the end of the URL. This uniquely identifes a video
      // at YouTube, so this is what we'll store 

      // TODO check that the URL provided is a valid one 
      let videoId = this.url.split('?v=')[1]   

      if (!this.url) {
        this.errors.push('Enter a video URL')
      }
      
      if (this.url && !videoId) {
        this.errors.push("Please check video URL")
      }

      if (this.errors.length === 0) {
        let activity = { title: this.title, youtubeId: videoId }
          this.$emit('new-activity', activity)
          this.title = ''
          this.url = ''
        } 
    }
  }
}

</script>

<style scoped>

  .error {
    color: rgb(114, 9, 9);
  }

  input {
    width: 60%;
    margin: 5px 10px;
  }

  label {
    width: 30%;
    margin: 5px 10px;
  }

  #add {
    margin: 20px;
    padding: 5px;
    background: rgb(231, 211, 163);
    padding-bottom: 40px;
  }

</style>