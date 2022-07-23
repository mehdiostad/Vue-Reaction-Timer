<template>
  <p class="score">Your Reaction Time: {{ score[score.length - 1] }}s !</p>
  <div class="rankAwsome" v-if="awsome">
    <p>{{ rank }}</p>
  </div>
  <div class="rankNotBad" v-if="notBad">
    <p>{{ rank }}</p>
  </div>
  <div class="rankTryAgain" v-if="tryAgain">
    <p>{{ rank }}</p>
  </div>
  <div class="ranking" v-if="showRanks">
    <h2>Your Best Scores are:</h2>
    <ul class="list">
      <li>{{ Math.min(...min) }}</li>
      <li v-if="showSecond">{{ second }}</li>
      <li v-if="showThird">{{ third }}</li>
    </ul>
  </div>
</template>

<script>
export default {
  props: ["score", "min"],
  data() {
    return {
      rank: null,
      showRanks: false,
      awsome: false,
      notBad: false,
      tryAgain: false,
      first: Math.min(...this.min),
      second: this.min[this.min.length - 2],
      third: Math.max(...this.min),
      showThird: true,
      showSecond: true,
    };
  },
  mounted() {
    this.handleRanksBox();
    if (this.score[this.score.length - 1] < 0.28) {
      this.rank = "Awsome!";
      this.awsome = true;
    } else if (this.score[this.score.length - 1] <= 0.4) {
      this.rank = "Not Bad...";
      this.notBad = true;
    } else {
      this.rank = "Try Again...";
      this.tryAgain = true;
    }
  },
  methods: {
    handleRanksBox() {
      if (this.min[2]) {
        this.showRanks = true;
        if (this.second == this.third) {
          this.showThird = false;
        }
        if (this.second == this.first) {
          this.showSecond = false;
        }
      }
    },
  },
};
</script>

<style>
.list {
  list-style-type: none;
}
.score {
  background: red;
  padding: 30px 45px;
  border-radius: 10px;
  color: white;
  font-size: 36px;
  width: 270px;
  margin: 20px auto;
  align-content: center;
  justify-content: center;
  display: flex;
  flex-direction: center;
}
.rankAwsome {
  background: rgb(34, 98, 34);
  padding: 10px;
  width: 350px;
  margin: 20px auto;
  border-radius: 7px;
  color: aliceblue;
}
.rankNotBad {
  background: rgb(170, 170, 19);
  padding: 10px;
  width: 350px;
  margin: 20px auto;
  border-radius: 7px;
  color: aliceblue;
}
.rankTryAgain {
  background: rgb(121, 37, 37);
  padding: 10px;
  width: 350px;
  margin: 20px auto;
  border-radius: 7px;
  color: aliceblue;
}
</style>
