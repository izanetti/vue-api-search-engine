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
        <div class="recent-post">
          <div class="recent-post-title">
            Guide to rendering points on a Google Map
          </div>
          <div class="recent-post-category">
            JavaScript
          </div>
        </div>
        <div class="recent-post">
          <div class="recent-post-title">
            Guide to rendering points on a Google Map
          </div>
          <div class="recent-post-category">
            JavaScript
          </div>
        </div>
        <div class="recent-post">
          <div class="recent-post-title">
            Guide to rendering points on a Google Map
          </div>
          <div class="recent-post-category">
            JavaScript
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'Homepage',
  data() {
    return {
    }
  },
  methods: {
    submitQuery(evt) {
      console.log(evt.target.value);
      this.$router.push({ name: 'SearchResults', params: { query: evt.target.value } })
    }
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
  grid-gap: 2.5rem;
}

.recent-post-title {
  color: #535353;
  font-size: 1.4rem;
}

.recent-post-category {
  color: #999999;
  font-size: 1.2rem;
  font-weight: 600;
}
</style>