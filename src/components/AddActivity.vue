<template>
  <div id="add">
    
    <h2>Add New Activity</h2>
    <p class="error" v-show="error" v-for="error in errors" v-bind:key="error"> {{ error }} </p>

    <label for="title">Title </label>
    <input id="title" v-model="title">
<br>
    <label for="youtube-url">Youtube URL</label>
    <input id="youtube-irl" v-model="url">
<br>
  <button v-on:click="add">Add</button>
 
  </div>
</template>

<script>

export default {
  name: 'AddActivity',
  data() { return  {
    title: '',
    url: '',
    errors: ''
  }},
  methods: {
    add() {

      this.errors = []

      if (!this.title) {
        this.errors.push('Enter a title')
      }

      let videoId = this.url.split('?v=')[1]   // hacky

      if (!this.url) {
        this.errors.push('Enter a URL')
      }
      
      if (!videoId) {
        this.errors.push("Please check video URL")
      }

      if (this.errors.length === 0) {
      let activity  = { title: this.title, youtubeId: videoId}
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
  width: 70%;
  margin: 5px 20px;
}

#add {
  margin: 20px;
  padding: 5px;
  background: rgb(231, 211, 163);
  padding-bottom: 40px;
}

</style>