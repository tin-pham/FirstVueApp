<template>
  <div class="box" v-if="isShowing" @click="stopTimer">Click Me</div>
</template>

<script>
export default {
  data() {
    return {
      timeBeforeShowing: this.getRandomTime(),
      isShowing: false,
      timer: null,
      currentTime: 0,
    };
  },
  mounted() {
    console.log('The box have been mounted');
    setTimeout(() => {
      this.isShowing = true;
      this.startTimer();
    }, this.timeBeforeShowing);
  },
  update() {
    console.log('Your time click was ' + this.currentTime);
  },
  methods: {
    getRandomTime() {
      return 2000 + Math.random() * 3000;
    },
    startTimer() {
      this.timer = setInterval(() => {
        this.currentTime += 10;
      }, 10);
    },
    stopTimer() {
      clearInterval(this.timer);
      this.isShowing = false;
      this.$emit('end', this.currentTime);
    },
  },
};
</script>

<style>
.box {
  background: hsl(180, 50%, 50%);
  display: flex;
  justify-content: center;
  align-items: center;
  border-radius: 1em;
  width: 300px;
  height: 300px;
  margin-inline: auto;
  color: white;
  font-family: sans-serif;
  font-size: 3rem;
  font-weight: bold;
}
</style>
