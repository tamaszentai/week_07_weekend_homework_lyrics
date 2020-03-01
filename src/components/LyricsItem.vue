<template lang="html">
  <div>
    <p>{{currentLyrics}}
    </p>
    <button @click="saveLyrics">Save Lyrics</button>
  </div>
</template>

<script>
import { eventBus } from '../main.js'

export default {
  name: 'lyrics-item',
  props:['currentLyrics'],
  methods: {
    saveLyrics() {
      eventBus.$emit('lyrics-selected', this.currentLyrics)
    }
  }
}
</script>

<style lang="css" scoped>
</style>
