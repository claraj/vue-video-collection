<template>
  <div>

    <h3>{{activity.title}}</h3>
    
    <iframe class="video-frame" v-bind:src="youtubeEmbedUrl">
    </iframe>

    <div><a v-bind:href="youtubeWatchUrl">Watch at YouTube</a></div>

    <div id="opinion">
      <label for="like"> Do you like?</label>
      <input id="like" type="checkbox" v-model="activity.like" v-on:change="ratingChanged">

      <div id="like-icon"> 
        <img v-if="activity.like" src="@/assets/like.png">
        <img v-if="activity.like == false" src="@/assets/dislike.png">
        <img v-if="activity.like == undefined" src="@/assets/no_rating.png">    
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
  methods: {
      ratingChanged() {
          this.$emit('rating-changed', this.activity)
      }
  },
  computed: {
    youtubeEmbedUrl() {
      return `https://www.youtube.com/embed/${this.activity.youtubeId}`
    },
    youtubeWatchUrl() {
      return `https://www.youtube.com/watch?v=${this.activity.youtubeId}`
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