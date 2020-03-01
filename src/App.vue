<template>
  <div id="app">
    <meta charset="utf-8">
    <img src="./assets/logo.png" alt="">
    <h1>Retriever</h1>
    <ul>




      <li>Artist name:</li>
      <li>
        <input v-model="artist" placeholder="Artist">
      </li>
      <li>Song title:</li>
      <li>
        <input v-model="title" placeholder="Song Name">
      </li>
      <li>
        <button @click="getlyrics">Get Lyrics</button>
      </li>
    </ul>
    <div>

      <p v-if="getlyrics">{{this.artist}}-{{this.title}}</p>
    <lyrics-box :lyrics="lyrics"></lyrics-box>
    </div>
  </div>

</template>

<script>
import {eventBus} from './main.js';
import LyricsBox from './components/LyricsBox.vue'
import LyricsItem from './components/LyricsItem.vue'


export default {
  name: 'App',
  data() {
    return {
      lyrics: [],
      savedLyrics: []
    }
  },
  mounted() {
    eventBus.$on('lyrics-selected', (currentLyrics) => { //NEW
      this.savedLyrics.push({
        Artist: this.artist,
        Title: this.title,
        Lyrics: currentLyrics})
      })
},
  components: {
  "lyrics-box": LyricsBox

  },
  methods: {
    getlyrics: function(artist, title) {
    fetch(`https://api.lyrics.ovh/v1/${this.artist}/${this.title}`)
    .then(res => res.json())
    .then(lyrics => this.lyrics = lyrics)
  },

  }
}
</script>

<style>
body {
  background-color: #383A3F;
}
img {
  height: 100px;
}

ul {
  list-style-type: none;
  margin: 20px;
  padding: 10px;
  overflow: hidden;
  background-color: #333333;
}

li {
  float: left;
  padding: 10px;
}

p {
  margin: 20px;
}



#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #F6B352;
  margin-top: 60px;
}
</style>
