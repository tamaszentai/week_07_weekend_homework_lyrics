<template>
  <div id="app">
    <meta charset="utf-8">
    <img src="./assets/logo.png" alt="">
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
    <div v-if="this.lyrics">
      <p>{{this.artist}}-{{this.title}}</p>
      <lyrics-box :lyrics="lyrics"></lyrics-box>
    </div>
    <!-- <div v-if="this.lyrics.error">
      <p>{{this.lyrics.error}}</p>
    </div> -->
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
      lyrics: null,
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
  background-color: #D9D4CF;
}
img {
  height: 100px;
}

ul {
  list-style-type: none;
  margin-top: 20px;
  margin-left: 25em;
  margin-right: 25em;
  padding: 10px;
  overflow: hidden;
  background-color: #7C7877;
  color: white;
}

li {
  float: left;
  padding: 10px;
}

p {
  margin-left: 30em;
  margin-right: 30em;
}

#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: black;
  margin-top: 60px;
}
button {
  display: inline-block;
  padding: 3px 10px;
  font-size: 15px;
  cursor: pointer;
  text-align: center;
  text-decoration: none;
  outline: none;
  color: #1e2022;
  background-color: #f0f5f9;
  border: none;
  border-radius: 15px;
  box-shadow: 0 3px #383A3F;
}

button:hover {background-color: #c9d6de}

button:active {
  background-color: #c9d6de;
  box-shadow: 0 5px #666;
  transform: translateY(4px);
}

</style>
