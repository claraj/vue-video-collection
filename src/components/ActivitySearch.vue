<template>
  <div>

    <h2>Search</h2>
      <label for="search">Search query </label>
    <input id="search" v-model="query" v-on:input="search">
<br>
    <label for="only-like">Only show liked videos </label>
    <input id="only-like" type="checkbox" v-model="onlyLike" v-on:change="search">
  </div>
</template>

<script>

export default {
  name: 'ActivitySearch',
  data() {return {
    query: '',
    onlyLike: false
  }},
  methods: {
      search() {
          let searchOptions = { query: this.query, onlyLike: this.onlyLike }
          this.$emit('search-updated', searchOptions)
      }
  }
}
</script>

<style>


</style>