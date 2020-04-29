<template>
  <div id="app">

<div id="container">
    
    <div id="top">
      <div id="title">
         <h1>Activity Video Collection</h1>
      </div>

    <div id="add-activity">
      <AddActivity v-on:new-activity="newActivity"></AddActivity>
    </div>
</div>

    <div id="main">
      <ActivityBrowser v-bind:activities="activities" v-on:rating-changed="ratingChanged"></ActivityBrowser>
    </div>
</div>

<footer>Heart icons by <a target="_blank" href="https://icons8.com">Icons8</a></footer>

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
  data() {
    return  {
      activities: [
        {'title': 'Solve a rubik cube', youtubeId: 'R-R0KrXvWbc', },
        {'title': 'Make pancakes', youtubeId: 'FLd00Bx4tOk', like:true},
        {'title': 'Do a push up', youtubeId: 'ABbVpmubIGQ'}
      ]
    }
  },
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
      // find by id and replace like value  
      this.activities.forEach( a => {
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
    flex-direction: column;
  }

  #top {
    display: flex;
    justify-content: center;
    align-items: center;
    flex-wrap: wrap;
    justify-content: space-around;
  }

  #title {
    flex-basis: 40%;
  }

  #add-activity {
    flex-basis: 60%;
  }

  #activity-browser {
    flex-grow: 1.1;
  }

</style>
