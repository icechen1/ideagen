<template>
  <div id="app" class="app">
    <div class="app__panel app__panel--left left_panel">
      <div class="left_panel__col_1">
        <controls class="left_panel__col_1__controls"></controls>
        <div class="left_panel__col_1__footer">
          <a href="https://medium.com/@accannis/generating-ideas-at-apple-71e575a1e2e3#.q2h6072jo" target="_blank">What is this?</a>
        </div>
      </div>
      <div class="left_panel__col_2">
        <div class="toggle_notepad" v-on:click="toggleNotepad()">
          <i class="fa fa-pencil-square-o"></i>
        </div>
      </div>
    </div>
    <div class="app__panel app__panel--right app__panel--{{notepadStyle}}" v-show="notepad" transition="expand">
      <div class="notepad" contenteditable="true">
        You can write notes here. Nothing is saved however, so remember to back this up!
      </div>
    </div>
    <!-- http://ellisonleao.github.io/sharer.js/ -->
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
  height: 100vh;
  width: 100vw;
  padding:0;
  margin:0;
}

.app {
  display: flex;
  flex-direction: row;
  justify-content: center;
  width: 100%;
  height: 100%;
  transition: flex-grow 1000ms linear;
  
  &__panel {
      height: 100%;
      flex: 1;
      overflow: hidden;
      transition: all 500ms linear;
       
      &--left {
        display: flex;
        align-items: center;
        justify-content: space-between;
        flex-direction: row;
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

.left_panel {
  &__col_1 {
    flex-grow: 2;
    display: flex;
    flex-direction: column;
    justify-content: space-between;
        
    &__controls {
    }
    
    &__footer {
      position: absolute;
      bottom: 0;
      text-align: center;
      width:100%;
    }
  }
  
  &__col_2 {
  }
}

.toggle_notepad {
  align-self: flex-end;
  border-radius: 8px 0px 0px 8px;
  padding: 20px 0px 20px 20px;
  background: #eee;
  i {
    font-size: 3em;
  }
}

.notepad {
  padding: 16px;
  outline: none;
  height: 100%;
}
/** Mobile **/

@media only screen
  and (max-device-width: 768px) {
    .toggle_notepad{
      display:none;
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
