<template>
  <h1>{{ title }}</h1>
  <button class="button" :disabled="isPlaying" @click="startGame">Start</button>
  <Box v-if="isPlaying" @end="endGame" />
  <Result :score="score" v-if="showResult" :showResult="showResult">
    <span>Your score is</span>
  </Result>
  <Result class="score--best" :bestScore="bestScore">
    <span>Your best score is</span>
  </Result>
</template>

<script>
import Box from './components/Box.vue';
import Result from './components/Result.vue';

export default {
  name: 'App',
  components: { Box, Result },
  data() {
    return {
      title: 'Reaction Timer',
      isPlaying: false,
      showResult: false,
      score: 0,
      bestScore: null,
    };
  },
  methods: {
    startGame() {
      this.isPlaying = true;
      this.showResult = false;
      // Random time when the game is start
    },
    endGame(timeAchived) {
      this.isPlaying = false;
      this.showResult = true;
      this.score = timeAchived;
      this.bestScore = this.getBestScore();
    },
    getBestScore() {
      if (!this.bestScore) {
        this.bestScore = this.score;
      }
      return this.score < this.bestScore ? this.score : this.bestScore;
    },
  },
};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
.button {
  padding: 0.75em 1.25em;
  text-transform: uppercase;
  cursor: pointer;
}
.score--best {
  position: absolute;
  bottom: 2em;
  left: 50%;
  transform: translateX(-50%);
}
</style>
