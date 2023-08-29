<template>
  <div> 
    <h1>Vue 3 Concepts Experiment</h1>
    <!--v-if, v-else, v-show, v-for, v-if with v-for -->
    <!-- Conditional Rendering -->
    <div>
      <h2>Conditional Rendering:</h2>
      
<!-- - v-if and v-else -->
      <button @click="toggleIf = !toggleIf">Toggle If</button>
      <p v-if="toggleIf">if toggle is true show this text!</p>
      <p v-else>else show this text</p>
      <br>
<!-- v-show -->
      <button @click="toggleShow">Toggle Show</button>
      <p v-show="showText">This paragraph is shown when v-show is true.</p>
    </div>
    <br><br>
    <!-- v-for with v-if -->
    <div @mouseover="toggleItems" @mouseleave="toggleItems">
      Hover over me to toggle items using v-if with v-for
    </div>

    <div v-for="element in itemss" :key="element.id">
      <p v-if="element.show">{{ element.text }}</p>
    </div>


<!-- v-for -->
    <div id="game">
      <h2>v-for example</h2>
      <h3>Tic Tac Toe</h3>
      <div v-for="(row, i) in board" :key="i" class="board-row">
      <button v-for="(cell, j) in row" :key="j" @click="makeMove(i, j)" class="game-button">
      {{ cell }}
      </button>
      </div>
      <h2>{{ message }}</h2>
      <button @click="resetBoard" class="reset-button">Start Over</button>
    </div>

  


    <!-- Form Input Handling -->
    <div>
      <h2>Form Input Handling:</h2>
      <label for="inputField">Enter something:</label>
      <input v-model="inputValue" id="inputField" />

      <p>You entered: {{ inputValue }}</p>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      showParagraph: true,
      showWithShow: true,
      items: ['Vue.js', 'React', 'Angular', 'Svelte'],
      inputValue: '',
      toggleIf: true,
      showText: false,
      board: Array(3).fill().map(() => Array(3).fill(null)),
      xIsNext: true,
      message: 'Next player: X',
      itemss: [
        { id: 1, text: 'Item 1', show: true },
        { id: 2, text: 'Item 2', show: false },
        { id: 3, text: 'Item 3', show: true },],
      };
      },

      



      methods: {
        toggleShow() {
      this.showText = !this.showText;},

      toggleItems() {
      this.itemss.forEach(element => {
        element.show = !element.show; 
      });},

      checkWinner() {
      const lines = [
      [0, 0, 0, 1, 0, 2],
      [1, 0, 1, 1, 1, 2],
      [2, 0, 2, 1, 2, 2],
      [0, 0, 1, 0, 2, 0],
      [0, 1, 1, 1, 2, 1],
      [0, 2, 1, 2, 2, 2],
      [0, 0, 1, 1, 2, 2],
      [0, 2, 1, 1, 2, 0]
      ];
      for (let line of lines) {
      const [a, b, c, d, e, f] = line;
      if (
      this.board[a][b] &&
      this.board[a][b] === this.board[c][d] &&
      this.board[a][b] === this.board[e][f]
      ) {
      return this.board[a][b];
      }
      }
      return null;
      },
      makeMove(i, j) {
      if (this.board[i][j] || this.checkWinner()) {
      return;
      }
      this.board[i][j] = this.xIsNext ? 'X' : 'O';
      this.xIsNext = !this.xIsNext;
      const winner = this.checkWinner();
      if (winner) {
      this.message = 'Winner: ' + winner;
      } else {
      this.message = 'Next player: ' + (this.xIsNext ? 'X' : 'O');
      if (!this.xIsNext) {
      this.$nextTick(() => {
      this.makeComputerMove();
      });
      }
      }
      },
      makeComputerMove() {
      let available = [];
      for (let i = 0; i < 3; i++) {
      for (let j = 0; j < 3; j++) {
      if (!this.board[i][j]) {
      available.push([i, j]);
      }
      }
      }
      if (available.length) {
      const move = available[Math.floor(Math.random() * available.length)];
      this.makeMove(move[0], move[1]);
      }
      },
      resetBoard() {
      this.board = Array(3).fill().map(() => Array(3).fill(null));
      this.xIsNext = true;
      this.message = 'Next player: X';
    }
  }
};
</script>

<style>
.game-button{
    width: 70px;
    height: 70px;
    cursor: pointer;
    padding: 0px;
    margin: 0px;
}
.reset-button{
    cursor: pointer;
}

</style>
