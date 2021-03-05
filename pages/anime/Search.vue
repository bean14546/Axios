<template>
  <div>
    <div>
      <v-text-field v-model="search" label="Search"></v-text-field>
      <v-btn @click="searchAnime">Search</v-btn>
    </div>
    <v-divider class="mt-1 mb-2"></v-divider>

    <div class="d-flex flex-wrap">
      <v-card v-for="search in results"
        :key="search.mal_id" class="ma-2" max-width="344" outlined>
        <v-list-item three-line>
          <v-list-item-content>
            <div class="overline mb-4">OVERLINE</div>
            <v-list-item-title class="headline mb-1">{{search.title}}</v-list-item-title>
            <v-list-item-subtitle>
              {{search.synopsis}}
            </v-list-item-subtitle>
          </v-list-item-content>

         <img class="img" :src="search.image_url" :style="{width: '80px', marginTop:'10px'}">
        </v-list-item>

      </v-card>
    </div>
  </div>
</template>
<script>
import axios from 'axios'
export default {
  data() {
    return {
      search: '',
      results: [],
    }
  },

  methods: {
    searchAnime() {
      const url = `https://api.jikan.moe/v3/search/anime?q=${this.search}&page=1`
      axios.get(url).then((res) => {
        this.results = res.data.results
      })
    },
  },
}
</script>
<style>

</style>
