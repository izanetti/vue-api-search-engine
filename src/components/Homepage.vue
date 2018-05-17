<template>
  <div>
    <h2>Homepage</h2>

    <input type="text" @keyup.enter="submitQuery">
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

</style>