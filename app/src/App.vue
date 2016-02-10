<template>
  <div id="app" class="app">
    <h1>Hello. What are you trying to brainstorm today?</h1>
    <input type="text" class="app__theme" placeholder="enter a problem statement" v-model="problem" />
    <random-word v-if="show" transition="expand"></random-word> <!-- use random color for card -->
  </div>
</template>

<script>
import RandomWord from './components/RandomWord'
export default {
  components: {
    RandomWord
  },

  computed: {
    show () {
      return this.problem
    }
  },

  data () {
    return {
      problem: undefined
    }
  }
}
</script>

<style lang="sass">
@import url(https://fonts.googleapis.com/css?family=Open+Sans);

$white: #fff;
$black: #000;

body {
  font-family: 'Open Sans', sans-serif;
  display: flex;
  align-items: center;
  height: 100vh;
  width: 100vw;
  padding:0;
  margin:0;
}

.app {
  display: flex;
  align-items: center;
  justify-content: center;
  flex-direction: column;
  width:100%;
  transition: flex-grow 1000ms linear;
  
  &__theme {
    width: 500px;
    background: transparentize($black, 0.8);
    color: $white;
    padding: 15px 0 15px 12px;
    border-radius: 8px;
    border: none;
    transition: all .3s ease-in-out;
    font-size: 24px;
    outline: none;
    text-align: center;
    &::placeholder {
      color: transparentize($white, 0.5);
    }
  }
}

/** Animations used by Vue **/
/* always present */
.expand-transition {
  transition: 0.5s ease-in-out;
}

/* .expand-enter defines the starting state for entering */
/* .expand-leave defines the ending state for leaving */
.expand-enter, .expand-leave {
  height: 0;
  padding: 0 10px;
  opacity: 0;
}
</style>
