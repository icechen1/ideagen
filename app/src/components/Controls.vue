<template>
  <div class="controls">
    <h1>{{ headerMessage }}</h1>
    <input type="text" class="controls__theme-box" placeholder="enter a problem statement" v-model="problem" />
    <random-word v-if="show" transition="expand"></random-word> <!-- use random color for card -->
  </div>
</template>

<script>
import RandomWord from './RandomWord'

export default {
  components: {
    RandomWord
  },

  computed: {
    show () {
      return this.problem
    },
    headerMessage () {
      if (this.problem === undefined || this.problem.length === 0) {
        return 'Hello. What are you trying to brainstorm today?'
      } else {
        return 'My problem statement is'
      }
    }
  },

  data () {
    return {
      problem: undefined
    }
  }
}
</script>

<style lang="sass" scoped>
$white: #fff;
$black: #000;

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
</style>

