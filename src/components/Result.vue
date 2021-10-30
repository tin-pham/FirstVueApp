<template>
  <div class="result">
    <p>
      <slot></slot> <span v-if="score"> {{ score }}ms</span> <span v-if="bestScore"> {{ bestScore }}ms </span>
    </p>
    <p v-if="score">{{ rank }}</p>
  </div>
</template>

<script>
export default {
  props: ['score', 'bestScore'],
  data() {
    return {
      scores: [],
      rank: this.getRank(),
    };
  },
  methods: {
    getRank() {
      if (this.score <= 250) {
        return 'God Level';
      }
      if (this.score < 285) {
        return 'Excellent';
      }

      if (this.score < 325) {
        return 'Good job';
      }

      return 'Need to practice more!!!';
    },
  },
};
</script>

<style></style>
