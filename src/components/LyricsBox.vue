<template lang="html">
  <div>
      <lyrics-item v-for="(currentLyrics,index) in lyrics" :currentLyrics="currentLyrics" :key="index">
      </lyrics-item>
</div>
</template>

<script>
import LyricsItem from './LyricsItem.vue'

export default {
  name: 'lyrics-box',
  props: ['lyrics'],


  methods: {

  },
  components: {
    "lyrics-item": LyricsItem
  }
}
</script>

<style lang="css" scoped>

</style>
