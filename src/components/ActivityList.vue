<template>
  <div>
    <h2>Video List</h2>

    <p id="count">{{ numberOfItems }} Activity Video(s)</p>

    <ActivityItem v-for="activity in activities" 
      v-bind:activity="activity"
      v-bind:key="activity.videoId"
      v-on:rating-changed="ratingChanged">
    </ActivityItem>
    
  </div>
</template>

<script>

import ActivityItem from '@/components/ActivityItem.vue'

export default {
  name: 'ActivityList',
  components: {
    ActivityItem
  },
  props: {
    activities: Array
  },
  methods: {
      ratingChanged(activity) {
          this.$emit('rating-changed', activity)
      }
  },
  computed: {
    numberOfItems() {
      return this.activities.length
    }
  }
}

</script>

<style scoped>

#count {
  border: 1px darkgreen solid;
  border-radius: 5px;
  display: inline-block;
  padding: 5px 30px
}

</style>