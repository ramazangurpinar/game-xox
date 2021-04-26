<template>
  <div>
    <div class="instructions">
      <h1>{{ message }}</h1>
    </div>
    <div class="game-board">
      <p v-if="winner"> Game is over! {{ winner }}</p>
      <table v-if="!winner" cellspacing="0">
        <tr class="row">
          <td class="cell" v-on:click="click(0,0)"> 
            {{ game[0][0] }} 
          </td>
          <td class="cell" v-on:click="click(0,1)"> 
            {{ game[0][1] }} 
          </td>
          <td v-on:click="click(0,2)"> 
            {{ game[0][2] }} 
          </td>
        </tr>
        <tr class="row">
          <td class="cell" v-on:click="click(1,0)"> 
            {{ game[1][0] }} 
          </td>          
          <td class="cell" v-on:click="click(1,1)"> 
            {{ game[1][1] }} 
            </td>          
          <td v-on:click="click(1,2)"> 
            {{ game[1][2] }} 
            </td>          
        </tr>
        <tr>
          <td class="cell" v-on:click="click(2,0)"> 
            {{ game[2][0] }} 
          </td>          
          <td class="cell" v-on:click="click(2,1)"> 
            {{ game[2][1] }} 
          </td>          
          <td v-on:click="click(2,2)"> 
            {{ game[2][2] }} 
          </td>          
        </tr>
      </table>
    </div>
  </div>
</template>

<script>
export default {
  name: 'Game',
  methods: {
    isDone: function isDone() {
      for (let i = 0; i < 3; i++)
        if(this.game[i][0] && this.game[i][0] === this.game[i][1] && this.game[i][0] === this.game[i][2]) return true;

      for (let i = 0; i < 3; i++)
        if(this.game[0][i] && this.game[0][i] === this.game[1][i] && this.game[0][i] === this.game[2][i]) return true;

      if(this.game[0][0] && this.game[0][0] === this.game[1][1] && this.game[0][0] === this.game[2][2]) return true;
      if(this.game[0][2] && this.game[0][2] === this.game[1][1] && this.game[0][2] === this.game[2][0]) return true;

      let emptyCount = 0;
      for (let i = 0; i < 3; i++) {
        for (let k = 0; i < 3; i++) {
          if(this.game[i][k] === '')
            emptyCount++;
        }        
      }

      if(!emptyCount) {
        return true;
      }
    },
    moveComputer: function moveComputer() {
      let x;
      let y;
      while(true){
        const randomX = Math.floor(Math.random() * 3);
        const randomY = Math.floor(Math.random() * 3);
        if(this.game[randomX][randomY] === ''){
          this.game[randomX][randomY] = 'O';
          break;
        }
      }
    },
    click: function click(x,y) {
      this.game[x][y] = 'X';
      this.$forceUpdate();
      if(this.isDone()){
        this.winner = 'X';
      } else {
        this.moveComputer();
        if(this.isDone()){
          this.winner = 'O';
        }
      }      
    }
  },
  data: function () {
    return {
      message: 'How To Play?',
      winner: false,
      clicks: 0,
      game: [
        // ['X','O','X'],
        // ['X','O','X'],
        // ['X','O','X'],
        ['','',''],
        ['','',''],
        ['','',''],        
      ]
    }
  },
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h3 {
  margin: 40px 0 0;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
a {
  color: #42b983;
}
.game-board table {
  margin: 0 auto;
}
.game-board table .row td {
  border-bottom: 1px solid black;
}
.game-board table tr .cell{
  border-right: 1px solid black;
}
.game-board td{
  width: 40px;
  height: 40px;
  line-height: 40px;
  text-align: center;
}

</style>
