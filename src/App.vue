<template>

  <div id="app">
    <meta charset="utf-8">
    <h1>Lyrics retriever</h1>
    <input v-model="artist">
    <input v-model="title">
    <button @click="getLyrics">Get Lyrics</button>
    {{ lyrics }}
  </div>
</template>

<script>


export default {
  name: 'App',
  data() {
    return {
      lyrics: []
    }
  },
  components: {

  },
  methods: {
    getLyrics: function(artist, title) {
    fetch(`https://api.lyrics.ovh/v1/${this.artist}/${this.title}`)
    .then(res => res.json())
    .then(lyrics => this.lyrics = lyrics)
    }
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
