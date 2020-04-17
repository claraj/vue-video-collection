<template>
  <div id="browser">
    <ActivitySearch v-on:search-updated="search"></ActivitySearch>
    <ActivityList v-bind:activities="displayActivities" v-on:rating-changed="ratingChanged"></ActivityList>
  </div>
</template>

<script>
import ActivitySearch from '@/components/ActivitySearch.vue'
import ActivityList from '@/components/ActivityList.vue'

export default {
  name: 'ActivityBrowser',
  components: {
    ActivitySearch,
    ActivityList
  },
  props: {
      activities: Array
  },
  data() { return  {
    displayActivities: [],
    searchOptions: {}
  }},
  mounted() {
    this.displayActivities = this.activities;
  },
  methods: {
      search(searchOptions) {

        this.searchOptions = searchOptions
        
        let filteredActivities = this.activities

        if (searchOptions.query) {
          filteredActivities = this.activities.filter( a => {
              return a.title.toLowerCase().includes(searchOptions.query.toLowerCase())
          })
        }

        if (searchOptions.onlyLike) {
          filteredActivities = filteredActivities.filter( a => {
              return a.like
          })
        }

        this.displayActivities = filteredActivities

      },
      ratingChanged(activity) {
        this.$emit('rating-changed', activity)
        this.search(this.searchOptions)
      }
  }
}
</script>

<style scoped>
#browser {
  background: rgb(184, 222, 200);
  margin: 20px;
  padding: 5px;
}

</style>