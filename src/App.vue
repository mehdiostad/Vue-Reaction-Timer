<template>
  <h1>Reaction Timer</h1>
  <button
    @click="start"
    :disabled="isPlaying"
    class="play"
    :class="{ playing: isPlaying }"
  >
    Play
  </button>
  <Block v-if="isPlaying" :delay="delay" @end="showTimer" />
  <Results v-if="showResult" :score="score" :min="min" />
</template>

<script>
import Block from "./components/Block.vue";
import Results from "./components/Results.vue";
export default {
  name: "App",
  components: { Block, Results },
  data() {
    return {
      delay: null,
      isPlaying: false,
      score: [],
      showResult: false,
      min: [],
    };
  },
  methods: {
    start() {
      this.delay = 2000 + Math.random() * 5000;
      this.isPlaying = true;
      this.showResult = false;
    },
    showTimer(reactionTime) {
      this.score.push(reactionTime);
      this.isPlaying = false;
      this.showResult = true;
      this.min.push(Math.min.apply(Math, this.score));
      // console.log(this.score)
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
  color: #444;
  margin-top: 60px;
}
.play {
  padding: 20px 30px;
  background: greenyellow;
  border: none;
  border-radius: 8px;
  color: black;
  font-size: 36px;
  cursor: pointer;
  width: 360px;
}
.playing {
  padding: 20px 30px;
  background: greenyellow;
  border: none;
  border-radius: 8px;
  color: white;
  font-size: 36px;
  cursor: pointer;
  width: 360px;
}
h1 {
  padding: 20px 30px;
  width: 300px;
  height: 50px;
  background: rgb(196, 5, 5);
  justify-content: center;
  align-content: center;
  align-items: center;
  display: flex;
  flex-direction: center;
  margin: 20px auto;
  border-radius: 10px;
  color: aliceblue;
}
</style>
