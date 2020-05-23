<template>    
    <div>
      <div class="container">
        <div v-if="!isRunning" class="winner-div">
          <span v-if="hasWinner">{{winner}} : has won!</span>
          <span v-if="!hasWinner">No Winner!</span>
        </div>
        <div v-if="isRunning" class="player-div">Player: {{sign}}</div> 
        <button v-on:click="restart" class="restart-button">Restart</button>
      </div>  

       <div class="grid-container">
        <Square :value="values[0]" v-on:click.native="setValue(0)"/>
        <Square :value="values[1]" v-on:click.native="setValue(1)"/>
        <Square :value="values[2]" v-on:click.native="setValue(2)"/>
        <Square :value="values[3]" v-on:click.native="setValue(3)"/>
        <Square :value="values[4]" v-on:click.native="setValue(4)"/>
        <Square :value="values[5]" v-on:click.native="setValue(5)"/>
        <Square :value="values[6]" v-on:click.native="setValue(6)"/>
        <Square :value="values[7]" v-on:click.native="setValue(7)"/>
        <Square :value="values[8]" v-on:click.native="setValue(8)"/>
      </div> 
    </div>
</template>

<script>
import Square from './Square'
import Vue from 'vue'

export default {
  name: 'TicTacToe',
  components: {
    Square
  },
  data: function() {
    return {
      values: Array(9).fill(null), // board values
      player: true, // true = X, false = O 
      sign: "X", // current sign
      winner: String, 
      isRunning: true,
      hasWinner : false,
    }
  },
  methods: {
    setValue: function(index){
      if(this.values[index] == null && this.isRunning){

        this.sign = this.player ? "X" : "O";
        // need to use Vue.set because else the binding for array woundnt work
        Vue.set(this.values, index, this.sign);

        // check for winner
        if(this.checkWinner(this.sign))
        {
          this.winner = this.sign;
          this.isRunning = false;
          this.hasWinner = true;
        }

        // if there is no winner and it is filled, there is no winner
        else if(this.isFilled())
        {
          this.isRunning = false;
          this.hasWinner = false;
        }

        this.changePlayer()
      }
    },
    changePlayer: function(){
      this.player = !this.player
      this.sign = this.player ? "X" : "O";
    },
    checkWinner: function(sign){
      const arr = Array.from(Array(3), () => new Array(3));
      let counter = 0;

      // parse 1d arr to 2d to easier compare
      for(let i = 0; i < 3; i++){
        for(let j = 0; j < 3; j++){
          if(this.values[counter] != null){
            arr[i][j] = this.values[counter];
            counter++;  
          }
          else{
            counter++;
          }
        }
      }

      // check for 3er pairs
      if(arr[0][0] == sign && arr[0][1] == sign && arr[0][2] == sign){ return true; }
      if(arr[1][0] == sign && arr[1][1] == sign && arr[1][2] == sign){ return true; }
      if(arr[2][0] == sign && arr[2][1] == sign && arr[2][2] == sign){ return true; }

      if(arr[0][0] == sign && arr[1][0] == sign && arr[2][0] == sign){ return true; }
      if(arr[0][1] == sign && arr[1][1] == sign && arr[2][1] == sign){ return true; }
      if(arr[0][2] == sign && arr[1][2] == sign && arr[2][2] == sign){ return true; }

      if(arr[0][0] == sign && arr[1][1] == sign && arr[2][2] == sign){ return true; }
      if(arr[0][2] == sign && arr[1][1] == sign && arr[2][0] == sign){ return true; }

      return false;
    },

    // this part is very stupid, fucking javascript
    // it somehow lasted very long to get this...
    isFilled: function(){
      let bool = true;
      this.values.forEach(val => {
        console.log(val === null)
        if(val === null ){
          bool = false;
          return bool;
        }
      });
      return bool;
    },
    
    restart: function(){
      console.log("Restart")
      this.values = Array(9).fill(null);
      this.player = true;
      this.sign =  "X"; // current sign
      this.winner = String; 
      this.isRunning = true;
    }
  }
}
</script>

<style scoped>
    .grid-container {
        position: relative;
        display: grid;
        grid-template-columns: 1fr 1fr 1fr;
        grid-template-rows: 1fr 1fr 1fr;
        gap: 5px 5px;
        grid-template-areas: ". . ." ". . ." ". . .";
    }

    .restart-button {
      float: right;
      position: relative;
      top: 0;
      right: 0;

      width: 100px;
      height: 30px;
      background-color: rgb(0, 185, 99);
      border: 0px;
      color: white;
      font-weight: 600;
    }

    .restart-button:hover{
      background-color: rgb(0, 230, 122);
      transition: ease-in .1s;
    }

    .restart-button:focus{
      outline: none;
    }

    .player-div, .winner-div{
      float: left;

      text-align: center;
      width: 100px;
      font-weight: 600;
    }

    .container{
      width: 310px;
      height: 35px;
      position: relative;
    }
</style>
