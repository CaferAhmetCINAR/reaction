<template>
 <h1>Reaction Timer v2</h1>
 <button @click="start" :disabled="isPlaying">Play</button>
 <Block v-if="isPlaying"  :delay="delay" @end="endGame"/>
 
 <p v-if="showResults">Your Reaction time: {{ score }} ms</p>
 <Result v-if="showResults" :score="score"/>
</template>

<script>
import Block from './components/Block.vue'
import Result from './components/Result.vue'

export default {
  components: { Block, Result  },
  data() {
    return {
      isPlaying:false,
      delay:null,
      score:null,
      showResults:false
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
