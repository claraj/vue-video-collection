<template>
  <div>

    <h3>{{activity.title}}</h3>
    
    <iframe class="video-frame" v-bind:src="youtubeEmbedUrl">
    </iframe>

    <div><a v-bind:href="youtubeWatchUrl">Watch at YouTube</a></div>

    <div id="opinion">
      
      <label for="like">What's your rating? Check for like</label>
      
      <input id="like" type="checkbox" v-model="activityItem.like" v-on:change="ratingChanged">

      <div id="like-icon"> 
        <img v-if="activity.like" src="@/assets/like.png">
        <img v-else-if="activity.like == false" src="@/assets/dislike.png">
        <img v-else src="@/assets/no_rating.png">    
      </div> 
    </div>

  </div>
</template>

<script>

export default {
  name: 'ActivityItem',
  props: {
    activity: Object
  },
  data() {
    return {
      /* A copy of the activity object that belongs to this component. It's 
       not recommended to modify a prop, since that affect the data in the 
       parent component. */ 
      activityItem: this.activity
    }
  },
  methods: {
      ratingChanged() {
          this.$emit('rating-changed', this.activityItem)
      }
  },
  computed: {
    youtubeEmbedUrl() {
      return `https://www.youtube.com/embed/${this.activityItem.youtubeId}`
    },
    youtubeWatchUrl() {
      return `https://www.youtube.com/watch?v=${this.activityItem.youtubeId}`
    }
  }
}

</script>

<style scoped>

#opinion {
  display: flex;
  align-items: center;
  justify-content: center;
}

#like-icon {
  margin-left: 10px;
}

.video-frame {
  height: 315px;
  width: 420px;
  margin: auto;
}
</style>