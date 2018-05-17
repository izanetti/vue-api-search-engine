<template>
  <div>
    <h2>Search Results..</h2>
    <input type="text" :value="query" @keyup.enter="submitQuery">
    <div v-for="result in results" :key="result.id">
      <pre>{{ result }}</pre>
    </div>
  </div>
</template>

<script>
import axios from 'axios';

export default {
  name: 'SearchResults',
  data() {
    return {
      query: null,
      results: []
    }
  },
  beforeMount() {
    // this.results.push(1)
    // this.results.push(2)
    // this.results.push(5)
    // console.log(this.$route.params);
    this.query = this.$route.params.query;
    this.getResults(this.query);
  },
  methods: {
    getResults(q) {
      this.results = [];
      axios.get('https://api.dailysmarty.com/search', {
        params: {
          q
        }
      })
        .then(response => {
          console.log(response.data.posts);
          this.results.push(...response.data.posts);
        })
        .catch(error => {
          console.log(error);
        });
    },
    submitQuery(evt) {
      this.query = evt.target.value;
      this.getResults(evt.target.value);
    }
  },
}
</script>

<style scoped>

</style>