<template>
  <form @submit.prevent="searchItunes(searchText)">
    <input type="text" v-model="searchText" />
    <button @click="searchItunes(searchText)">Search</button>
    <div v-if="data.results">
      <div v-for="album in data.results" :key="album.artistId">
        <h3>Album Name: {{album.collectionName}}</h3>
        <h5>ArtWork</h5>
        <img :src="album.artworkUrl100" alt="">
        <h5>Price: {{album.collectionPrice}}</h5>
        <TheShowAlbum :album="album" />
      </div>
    </div>
  </form>
</template>

<script lang="ts">
import { defineComponent } from 'vue';
import {itunesSearch} from './services/iTunesAPI'
import {ItunesTypes} from './types/itunesTypes.interface'
import TheShowAlbum from './components/TheShowAlbum.vue'

export default defineComponent({
  name: 'App',
  components: {
    TheShowAlbum
  },
  data() {
    return {
      data: {} as ItunesTypes,
      searchText: ""
    }
  },
  methods: {
    async searchItunes(search: string): Promise<void> {
      const value = await itunesSearch(search)
      this.data = value
      console.log("data", this.data)
    }
  }
});
</script>

<style lang="scss">
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
