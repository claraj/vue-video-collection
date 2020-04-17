<template>
  <div id="search-form">

    <h2>Search</h2>

    <div class="form-input">
      <label for="search">Search query </label>
      <input id="search" v-model="query" v-on:input="search">
    </div>

    <div class="form-input">
    <label for="only-like">Only show liked videos </label>
    <input id="only-like" type="checkbox" v-model="onlyLike" v-on:change="search">
  </div>
  
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

<style scoped>

#search-form {
  /* border: 1px darkgreen solid;
  border-radius: 5px; */
  padding: 10px;
  background: rgb(165, 193, 165);
  
}

.form-input {
  margin: 5px 10px;
}


</style>