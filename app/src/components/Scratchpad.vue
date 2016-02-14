<template>
  <div class="random-word">
    <span class="random-word__word">{{ word }}</span>
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

<style lang="sass" scoped>
.random-word {
   align-self: center;
   
   &__word{
     font-size: 4em;
   }
}
</style>

