<template>
  <div class="block" v-if="showBox" @click="stopTimer">Click Me!</div>
</template>

<script>
export default {
  props: ["delay"],
  data() {
    return {
      showBox: false,
      reactionTimer: 0,
      time: null,
    };
  },
  mounted() {
    setTimeout(() => {
      this.showBox = true;
      this.startTimer();
    }, this.delay);
  },
  methods: {
    startTimer() {
      this.time = setInterval(() => {
        this.reactionTimer += 10;
      }, 10);
    },
    stopTimer() {
      clearInterval(this.time);
      this.reactionTimer /= 1000;
      this.$emit("end", this.reactionTimer);
    },
  },
};
</script>

<style>
.block {
  width: 400px;
  border-radius: 20px;
  background: #0faf87;
  color: white;
  text-align: center;
  padding: 100px 0;
  margin: 40px auto;
}
</style>
