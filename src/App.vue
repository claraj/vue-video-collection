<template>
  <div id="app">

    <h1>Activity Video Collection</h1>

<div id="container">
    <div id="add-activity">
      <AddActivity v-on:new-activity="newActivity"></AddActivity>
    </div>

    <div id="activity-browser">
      <ActivityBrowser v-bind:activities="activities" v-on:rating-changed="ratingChanged"></ActivityBrowser>
    </div>
</div>

  </div>
</template>

<script>
import ActivityBrowser from './components/ActivityBrowser.vue'
import AddActivity from './components/AddActivity.vue'

export default {
  name: 'App',
  components: {
    AddActivity,
    ActivityBrowser
  },
  data() {return  {
    activities: [
      {'title': 'spork', youtubeId: '12345', },
      {'title': 'goo', youtubeId: '12346', like:true},
      {'title': 'boop', youtubeId: '12347'}
    ]
  }},
  methods: {
    newActivity(activity) {
      // no duplicates
      if (this.activities.find( a => a.youtubeId ===activity.youtubeId )) {
        alert('You already added that video! Try another?') 
      } else {
        this.activities.push(activity)
      }
    },
    ratingChanged(activity) {
      // find by id and replace in array 
      console.log('log', activity.youtubeId)
      this.activities.forEach( a => {

      console.log('loop', a.youtubeId)
        if (a.youtubeId == activity.youtubeId) {
          a.like = activity.like 
        }
      })
    }
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  padding-top: 10px;
  background: rgb(238, 248, 255);
}

#container {
  display: flex;
  flex-wrap: wrap;
  justify-content: center;
}

#add-activity {
  
}

#activity-browser {
  flex-grow: 1.1;
}
</style>
