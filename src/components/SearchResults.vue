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
.results-search-bar input {
  height: 5rem;
  margin-bottom: 1em;
  margin-top: 3em;
}

.results-posts-wrapper {
  grid-row: 3;
  grid-column: 1/-1;
  width: 66vw;
}

.post {
  margin-top: 3em;
  margin-bottom: 3em;
}

.category-name {
  color: #2660f3;
  margin-bottom: 1.5rem;
  font-size: 1.4rem;
}

.result-post-title a {
  color: #535353;
  text-decoration: none;
  font-size: 1.8rem;
}

.result-post-links-wrapper {
  margin-top: 2rem;
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(100px, 1fr));
  grid-gap: 2rem;
}

.result-post-link {
  color: #535353;
  text-decoration: none;
  font-size: 1.4rem;
}

.result-post-link:hover {
  text-decoration: underline;
}

.results-logo {
  grid-row: 1;
  grid-column: 2;
  display: flex;
  justify-content: center;
  align-items: center;
}

.results-logo img {
  width: 50px;
}
</style>