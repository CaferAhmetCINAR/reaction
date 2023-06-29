<template>
  <h1>Reaction Timer v2</h1>
  <button @click="start" :disabled="isPlaying">Play</button>
  <Block v-if="isPlaying"  :delay="delay" @end="endGame"/>
  
  <p v-if="showResults">Your Reaction time: {{ score }} ms</p>
  <Result v-if="showResults" :score="score"/>
  <div style="display:flex; justify-content:center; margin-top:10px;" v-if="isPlaying==false">
    <table>
      <thead>
        <tr>
          <td>#</td>
          <td>reaction time (ms)</td>
        </tr>
      </thead>
      <tbody>
        <tr v-for="(item, index) in reactionTimes" :key="index">
          <td>{{ index+1 }}</td>
          <td>{{ item }} ms</td>
        </tr>
        <tr v-if="reactionTimes.length==0">
          <td colspan="2">
            Hic skor girilmedi
          </td>
        </tr>
      </tbody>
    </table>
  </div>
</template>

<script>
import Block from './components/Block.vue'
import Result from './components/Result.vue'

export default {
  components: { Block, Result },
  data() {
    return {
      isPlaying:false,
      delay:null,
      score:null,
      showResults:false,
      reactionTimes: []
    }
  },
  methods: {
    start(){
      this.isPlaying=true
      this.delay= 2000 + Math.random() * 5000
      this.showResults=false
    },
    endGame(reactionTime){
      this.showResults=true
      this.score=reactionTime
      this.reactionTimes.push(reactionTime)
      this.isPlaying=false
    }
  },
}
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
button {
  color:aqua;
  background-color:black;
  padding: 10px 20px;
  font-size: 1.4em;
  border-color: aqua;
  font-style: italic;
  cursor: pointer;
}
button[disabled]
{
  opacity: 0.2;
  cursor: not-allowed;
}
</style>
