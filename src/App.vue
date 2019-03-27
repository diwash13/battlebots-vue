<template>
  <div id="app">
    <nav class='nav'>
    <button class='title' @click="toggle" >Create Bot</button>
    <h1>Battle Bots</h1>
    <button class='title' @click="toggle" >Collection</button>
    </nav>
    <section class="container" v-if='showForm' >
      <input  class='input' type="text" placeholder="Bot Name*" v-model="bot">
      <br>
      <input class='input' type="text" placeholder="Attack Value*" v-model="attack">
      <button @click="increment">+</button>
      <button @click="decrement">-</button>
      <br>
      <input class='input' type="text" placeholder="Health Value*" v-model="health">
      <button @click="inc">+</button>
      <button @click="dec">-</button>
      <br>
      <button @click='createBot'>Submit</button>
      <button>Clear</button>
      
    </section>
    <section v-else>
      <h3>Bot 1</h3>
      <h3 v-if="selectedBots[0]">Bot #1: {{selectedBots[0].bot}}</h3>
      <h3 v-if="selectedBots[1]">Bot #2: {{selectedBots[1].bot}}</h3>
      <button @click='battle' >Battle</button>
      <button @click="clearSelected">Clear</button>
      <hr>
      <bot v-for="(botObj, i) in allBots" 
        :key='i' 
        :index = 'i' 
        :bot-obj='botObj' 
        :retire-bot = 'retireBot'
        :selectBot = 'selectBot' 
        />
      <!-- <bot v-for='(bot, i) in allBots' :key='i' :index='i' :retireBot='retireBot' /> -->
    </section>
  </div>
</template>

<script>
import Bot from './components/Bot'
export default {
  name: 'app',
  data: function() {
    return {
      showForm: true,
      bot: '',
      attack: '',
      health: '',
      allBots: [
        {bot: 'Frank', attack: 30, health: 20},
        {bot: 'Harry', attack: 40, health: 10},
        {bot: 'Pearl', attack: 10, health: 40}
        ],
      selectedBots: []
    }
  },
  methods: {
    increment: function() {
      this.attack++
    },
    decrement: function() {
      this.attack--
    },
    inc: function() {
      this.health++
    },
    dec: function() {
      this.health--
    },
    toggle: function() {
      this.showForm = !this.showForm
    },
    createBot: function() {
      const newBot = {bot: this.bot, attack: this.attack, health: this.health}
      this.allBots.push(newBot)
      this.bot = ''
      this.attack = ''
      this.health = ''
      this.toggle()
  },
  retireBot: function (i) {
      this.allBots = this.allBots.filter((bot, index) => index !== i)
    },
    selectBot: function(newBot) {
      if (this.selectedBots.length < 2) {
        this.selectedBots.push(newBot);
      } else {
        alert('2 Bots Have Been Selected');
      }
  },
  clearSelected: function() {
    this.selectedBots = []
  },
  battle() {
      if (this.selectedBots[0].attack > this.selectedBots[1].attack) {
        alert(`${this.selectedBots[0].bot} wins!`);
      } else {
        alert(`${this.selectedBots[1].bot} wins!`);
      }
      this.selectedBots = [];
    }
  },
  components: {
    Bot: Bot
  }
}
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
  background-color: #00E498;
  height: 100vh;
}
.nav {
  display: flex;
  justify-content: space-evenly;
  color: white;
  background-color: #00336D;
  height: 100px;
  width: 100vw;
}
.title {
    font-size: 20px!important;
    font-weight: 500;
    line-height: 1!important;
    letter-spacing: .02em!important;
    background-color: #00336D;
    color: white;
}
.container {
    height: 300px;
    width: 500px;
    margin-top: 50px;
    margin-left: 400px;
    background-color: white;

}
.input {
    margin-top: 50px;
    height: 30px;
    width: 80%;
    font-family: -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, Oxygen, Ubuntu, Cantarell, 'Open Sans', 'Helvetica Neue', sans-serif;
    font-size: 20px;
}
</style>
