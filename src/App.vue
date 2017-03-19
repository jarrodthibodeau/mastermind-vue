<template>
  <div>
    <h1 id="mastermind"> Mastermind </h1>
    <div id="app">
      <div id="game">
        <GuessContainer :guesses="guesses" :clear="clear" :submit="submit" :replay="replay" :isClearing="isClearing" :statuses="statuses"/>
        <div class="button-container"> 
            <GameButton v-for="color in colors" :color="color" :guess="guess"/>
        </div>
      </div>
      <div id="guesses">
        <Guesses :attempts="attemptedAnswers"/>
      </div>
      <div id="rules">
        <Rules />
      </div>
    </div>
  </div>
</template>

<script>
import GameButton from './components/GameButton'
import GuessContainer from './components/GuessContainer';
import Guesses from './components/Guesses';
import Rules from './components/Rules';


export default {
  name: 'app',
  components: {
    GameButton,
    GuessContainer,
    Guesses,
    Rules
  },
  data: function() {
    return {
      colors: ['#FF0000', '#FF7400', '#009999', '#00CC00'],
      guesses: [],
      correctAnswer: [],
      gotAnswer: false,
      tries: 0,
      attemptedAnswers: [],
      isClearing: false,
      statuses: [-1, -1, -1, -1]
    }
  },
  methods: {
      guess: function(guess) {
        if (this.guesses.length < 4) {
          this.guesses.push(guess);
        }
      },
      submit: function(answer) {
        if (answer.length < 4) {
          alert('You need to have all 4 selected to submit');
        } else {
          for(let i = 0; i < answer.length; i++) {
            if (answer[i] === this.correctAnswer[i]) {
              this.statuses[i] = 1;
            } else if (this.correctAnswer.includes(answer[i])) {
              this.statuses[i] = 0;
            } else {
              this.statuses[i] = -1;
            }
          }

          this.attemptedAnswers.push(answer);
          this.clear();

          this.tries++;

          if (this.statuses.filter((s) => s === 1).length === 4) {
            return alert('You got the correct answer! Congratulations!');
          }

          if (this.tries >= 10) {
            return alert('Aw man, you were not able to get the answer in 10 tries! Try again!');
          }          
        }
      },
      clear: function() {
        if (this.guesses.length > 0) {
          var self = this;
          this.isClearing = true;

          setTimeout(function() {
            self.isClearing = false;
            self.guesses = [];
          }, 260);
        }
      },
      generateAnswer: function() {
        for (let i = 0; i < 4; i++) {
          this.correctAnswer.push(this.colors[Math.floor(Math.random() * 4)]);
        }

        console.log(this.correctAnswer);
      },
      replay: function() {
        this.statuses = [-1, -1, -1, -1];
        this.correctAnswer = [];
        this.generateAnswer();
        this.attemptedAnswers = [];
        this.gotAnswer = false;
        this.tries = 0;
      }
  },
  created: function () {
    this.generateAnswer();
  }
}
</script>

<style scoped>
@import url('https://fonts.googleapis.com/css?family=Exo');

#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
  display: flex;
  flex-flow: row wrap;
  width: 100%;
  height: 100%;
  transform: translateY(5%);
}

#game {
  width: 75%;
  height: 100%;
}

#extra {
  width: 17.5%;
}

#rules {
  display: flex;
  justify-content: center;
  width: 100%;
}

.button-container {
  display: flex;
  justify-content: center;
  flex-direction: row nowrap;
  margin-top: 3%;
  width: 100%;
}

#mastermind {
  text-align: center;
  font-size: 3em;
  font-family: 'Exo', sans-serif;
}

@media screen and (max-width: 1399px) {
  .button-container {
    width: 100%;
  }

  #extra {
    width: 10%;
  }
} 

@media screen and (max-width: 900px) {
  #app {
    flex-direction: column;
    margin-top: 0;
  }

  #game {
    flex-direction: column wrap;
    width: 100%;
  }

  #guesses {
    width: 100%;
  }
}

</style>
