<template>
  <div class="random-word">
    <span class="random-word__word">{{ word }}</span>
    <button class="random-word__new fa fa-refresh" v-on:click="chooseNewWord">New</button>
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
    width: 40%;
    min-width: 400px;
    display: flex;
    flex-direction: row;
    align-items: center;
    justify-content: space-between;
  
   &__word {
     font-size: 4em;
   }
   
   &__new {
      height:100%;
      background: none;
      color: green;
      padding: 15px 0 15px 12px;
      border: none;
      transition: all .3s ease-in-out;
      font-size: 24px;
      outline: none;
      text-align: center;
      align-self: flex-end;
   }
}
</style>

