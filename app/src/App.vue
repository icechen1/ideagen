<template>
  <div id="app" class="app">
    <div class="app__panel app__panel--left">
      <div class="controls">
        <h1>Hello. What are you trying to brainstorm today?</h1>
        <input type="text" class="controls__theme-box" placeholder="enter a problem statement" v-model="problem" />
        <random-word v-if="show" transition="expand"></random-word> <!-- use random color for card -->
      </div>
    </div>
    <div class="app__panel app__panel--right app__panel--added-in" v-if="notepad">
      Test
    </div>
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
      problem: undefined,
      notepad: false
    }
  }
}
</script>

<style lang="sass">
@import url(https://fonts.googleapis.com/css?family=Open+Sans);
@import './scss/font-awesome.scss';

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
  flex-direction: row;
  align-items: center;
  justify-content: center;
  width:100%;
  height: 100%;
  transition: flex-grow 1000ms linear;
  
  &__panel {
      height: 100%;
      flex: 1;
      overflow: hidden;
      transition: all 500ms linear;
      
      &--left {
        display: flex;
        flex-direction: column;
        align-items: center;
        justify-content: center;
        width:100%;
        height: 100%;
      }
      
      &--right {
        background: rgba(0, 0, 0, .6);
      }
      
      &--added-in {
        flex: .00001;
        animation: flexGrow 500ms ease forwards;
      }
      
      &--removed {
        flex: 1;
        animation: flexShrink 500ms ease forwards;
      }
  }
}

.controls{
  display: flex;
  flex-direction: column;
  align-items: center;
  &__theme-box {
    width: 40vw;
    min-width: 500px;
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

@keyframes flexGrow {
  to {
    flex: 1;
  }
}

@keyframes flexShrink {
  to {
    flex: .01;
    flex: .00001;
  }
}
</style>
