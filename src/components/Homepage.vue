<template>
  <div class="container container-homepage">
    <div class="homepage-logo">
      <img src="@/assets/ds_circle_logo.png" alt="">
    </div>

    <div class="search-bar homepage-search-bar">
      <input type="text" placeholder="&#xf002; Search DailySmarty" @keyup.enter="submitQuery">
      <p>Press return to search</p>
    </div>

    <div class="recent-posts-wrapper">
      <div class="recent-posts-heading">
        Recent Posts
      </div>

      <div class="recent-posts">
        <div v-for="post in recentPosts.slice(0, 3)" :key="post.id" class="recent-post">
          <div class="recent-post-title">
            <a :href="post.url_for_post" target="_blank">{{ post.title }}</a>
          </div>
          <div class="recent-post-category">
            {{ post.associated_topics[0] }}
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import axios from 'axios';

export default {
  name: 'Homepage',
  data() {
    return {
      recentPosts: []
    }
  },
  beforeMount() {
    this.getRecentPosts()
    console.log(this.recentPosts);
  },
  methods: {
    submitQuery(evt) {
      console.log(evt.target.value);
      this.$router.push({ name: 'SearchResults', params: { query: evt.target.value } })
    },
    getRecentPosts() {
      this.results = [];
      axios.get('https://api.dailysmarty.com/posts')
        .then(response => {
          console.log(response.data.posts);
          this.recentPosts.push(...response.data.posts);
        })
        .catch(error => {
          console.log(error);
        });
    },
  }
}
</script>

<style scoped>
.container-homepage {
  margin-top: 5em;
  align-items: center;
  height: 100vh;
}

.homepage-logo {
  grid-column: 2;
  grid-row: 1;
}

.homepage-logo img {
  width: 10.5rem;
}

.homepage-search-bar input {
  height: 11.8rem;
}

.recent-posts-wrapper {
  grid-column: 1/-1;
  grid-row: 3;
}

.recent-posts-heading {
  color: #2660f3;
  margin-bottom: 3rem;
  font-size: 1.4rem;
}

.recent-posts {
  display: grid;
  width: 66vw;
  grid-template-columns: repeat(auto-fit, minmax(100px, 1fr));
  grid-gap: 4rem;
}

.recent-post-title {
  margin-bottom: 15px;
}

.recent-post-title a {
  color: #535353;
  font-size: 1.4rem;
  text-decoration: none;
}

.recent-post-category {
  color: #999999;
  font-size: 1.2rem;
  font-weight: 600;
}
</style>