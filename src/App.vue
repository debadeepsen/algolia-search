<script>
export default {
  data() {
    return {
      query: '',
      results: []
    }
  },
  methods: {
    async algoliaSearch() {
      const url = `http://hn.algolia.com/api/v1/search?query=${this.query}`
      const data = await fetch(url).then((r) => r.json())
      this.results = data.hits.map((h) => h._highlightResult.title.value)
    }
  }
}
</script>

<template>
  <div>
    <div>
      <input type="text" v-model="query" @keyup="algoliaSearch" />
    </div>
    <div v-for="(r, i) in results" :key="i" style="margin-top: 4px;">
      <span v-html="r"></span>
      
    </div>
  </div>
</template>

<style scoped>
input {
  padding: 5px;
}
</style>
