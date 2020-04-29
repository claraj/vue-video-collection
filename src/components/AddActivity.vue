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

      let videoId 

      if (!this.title) {
        this.errors.push('Enter a title')
      }

      /* Example video URL is https://www.youtube.com/watch?v=aAxGTnVNJiE
      
      Notice the ID at the end of the URL. This uniquely identifes a video
      at YouTube, so this is what we'll store in an activity object
      In a URL, everything after a ? is a set of key=value pairs, often refered
      to as params, or parameters, or search parameters. 
      The search params in the examples URL above are 
      
      v=aAxGTnVNJiE
      
      We can use the built-in URL and URLSearchParams to extract the ID
      from the URL. 
      
      */

      if (!this.url) {
        this.errors.push('Enter a video URL')
      }

      else {  // there is a url, is it valid?
        try {
          let url = new URL(this.url)   
          let params = new URLSearchParams(url.search)
          videoId = params.get('v')  // key is the v in (for example) v=aAxGTnVNJiE
          if (!videoId) {
            this.errors.push('Enter a valid YouTube URL')
          }  
        }
        catch (TypeError) {  // thrown if the URL is not a valid format.  
          this.errors.push('Enter a valid YouTube URL')
        }
      }

      // Finally, if there are no errors detected... 
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