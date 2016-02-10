<template>
  <div class="random-word">
    <h1>{{ word }}</h1>
    <button v-on:click="chooseNewWord">New</button>
  </div>
</template>

<script>
var fileContent = require('../assets/wordlist.txt')

export default {
  data () {
    return {
      words: fileContent,
      index: 0
    }
  },

  methods: {
    chooseNewWord () {
      const fileContentLines = this.words.split('\n')
      const randomLineIndex = Math.floor(Math.random() * fileContentLines.length)
      this.index = randomLineIndex
    }
  },

  computed: {
    word () {
      return this.words.split('\n')[this.index]
    }
  },

  ready () {
    this.chooseNewWord()
  }
}
</script>

<style lang="sass">
.random-word {
   align-self: center;
}
</style>

