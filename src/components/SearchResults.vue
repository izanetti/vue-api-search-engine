<template>
  <div class="container container-results">
    <div class="results-logo">
      <router-link :to="{ name: 'Homepage' }">
        <img src="@/assets/ds_circle_logo.png" alt="">
      </router-link>
    </div>

    <div class="search-bar results-search-bar">
      <input type="text" placeholder="&#xf002; Search DailySmarty" :value="query" @keyup.enter="submitQuery">
    </div>

    <div class="results-posts-wrapper">
      <div v-if="gettingResults">
        <h2>Loading...</h2>
      </div>

      <div v-if="results.length > 0">
        <div v-for="result in results" :key="result.id" class="post">
          <div class="topic-wrapper">
            <span v-for="topic in result.associated_topics" :key="topic" class="category-name">
              {{ topic }}
            </span>
          </div>

          <div class="result-post-title">
            <a :href="result.url_for_post" target="_blank">
              {{ result.title }}
            </a>
          </div>

          <div v-if="result.post_links.length > 0" class="resource_links_wrapper">
            <div>Resource links</div>
            <div class="result-post-links-wrapper">
              <a v-for="resultPostLink in result.post_links" :key="resultPostLink.link_url" :href="resultPostLink.link_url" class="result-post-link" target="_blank">{{resultPostLink.link_url}}</a>
            </div>
          </div>
        </div>
      </div>

      <div v-if="!gettingResults && results.length == 0">
        <h2>There are no results for your query</h2>
      </div>

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
      results: [],
      showResourceLinks: false,
      gettingResults: true
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
      this.gettingResults = true;
      this.results = [];

      axios.get('https://api.dailysmarty.com/search', {
        params: {
          q
        }
      })
        .then(response => {
          console.log(response.data.posts);

          this.results.push(...response.data.posts);
          this.gettingResults = false;

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
  margin-bottom: 5em;
}

.topic-wrapper {
  margin-bottom: 10px;
  font-weight: 600;
}

.category-name {
  color: #2660f3;
  margin-right: 15px;
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

.resource_links_wrapper {
  margin-top: 10px;
}
</style>