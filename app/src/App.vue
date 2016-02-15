<template>
  <div id="app" class="app">
    <div class="app__panel app__panel--left">
      <controls></controls>
      <div class="app__panel__footer">
        <a href="https://medium.com/@accannis/generating-ideas-at-apple-71e575a1e2e3#.q2h6072jo" target="_blank">What is this?</a>
      </div>
      <div class="toggle_notepad" v-on:click="toggleNotepad()">
        <i class="fa fa-pencil-square-o"></i>
      </div>
    </div>
    <div class="app__panel app__panel--right app__panel--{{notepadStyle}}" v-show="notepad" transition="expand" contenteditable="true">
      http://ellisonleao.github.io/sharer.js/
    </div>
  </div>
</template>

<script>
import Controls from './components/Controls'

export default {
  components: {
    Controls
  },

  methods: {
    toggleNotepad () {
      this.notepad = !this.notepad
    }
  },

  computed: {
    notepadStyle () {
      return this.notepad ? 'added-in' : 'removed'
    }
  },

  data () {
    return {
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
        
      &__footer {
         position: absolute;
         bottom: 0;
         text-align: center;
         width:100%;
      }
      
      &--left {
        display: flex;
        align-items: center;
        justify-content: center;
        flex-direction: column;
        width: 100%;
        height: 100%;
        flex-grow: 1;
      }
      
      &--right {
        background: rgba(0, 0, 0, .05);
        font-size: 1.5em;
      }
      
      &--added-in {
        flex: .00001;
        animation: flexGrow 500ms ease forwards;
      }
      
      &--removed {
        flex: 2;
        animation: flexShrink 500ms ease forwards;
      }
  }
}

.toggle_notepad {
  align-self: flex-end;
  border-radius: 8px 0px 0px 8px;
  padding: 20px 0px 20px 20px;
  order: -1;
  background: #eee;
  i {
    font-size: 3em;
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
    flex: 2;
  }
}

@keyframes flexShrink {
  to {
    flex: .01;
    flex: .00001;
  }
}
</style>
