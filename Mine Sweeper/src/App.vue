<script>
export default {

  data() {
    return {
      minsSelected: null,
      selectedlLevel:12,
      level: {
        'easy': 12,
        'mid': 20,
        'hard': 31

      },
      title: 'akpevwe',
      BoardData: [],
      // type:1,
      class: 'bg-red-500',
      group: 2,
      isMines: [
        {
          false: 'bg-green-500',
          true: 'bg-red-500'
        },],
      gameLevel: 1
    }

  },

  methods: {
    generateBoard(level) {
      this.BoardData=[];
      this.minsSelected=null;
      for (let i = 0; i < level; i++) {
        const randomType = Math.floor(Math.random() * 2) + 1; // Generate random type (1, 2, or 3)
        const randomGroup = Math.floor(Math.random() * 3) + 1; // Generate random group (1, 2, or 3)
        const randomMines = Math.random() < 0.5; // Randomly assign mines property true or false
        const randomColorIndex = Math.floor(Math.random() * this.isMines.length); // Generate random index for isMines array
        const randomClass = this.isMines[0][randomMines]; // Select random color from colors array

        this.BoardData.push({
          type: randomType,
          class: randomClass, // Assign random color class
          group: randomGroup,
          isSelected: null,
          mines: randomMines,
        });
      }

    },

    select(index) {
      let selected = this.BoardData[index];
      if (selected.mines) {
       this.minsSelected= this.gameOver();
      }
      else{
        selected.isSelected=true;
        console.log('akpevwe')
      }
      // this.generateBoard();
      // console.log("game over");
      // selected==null;
    },
    gameOver(){
      return true
    }
  },
  computed:{
    changedlLevel(){
      return this.selectedlLevel

    }
  }
,

  mounted() {
    this.generateBoard(this.selectedlLevel);
  }
}
</script>

<template>

  <div class="container mx-auto p-6 bg-white rounded-lg shadow-md">
    <h1 class="text-3xl font-semibold text-center mb-6">Minesweeper</h1>

      <!-- Game cells with padding -->
      <div v-if="minsSelected"><div class="grid grid-cols-4 gap-4 mb-6">
      <button v-for="(board,index) in BoardData" class="cell bg-gray-300 border border-gray-400 p-4" v-text="board"
              :class="board.class"></button>
      </div>
    </div>

      <div v-else>
        <div class="grid grid-cols-4 gap-4 mb-6">
        <button v-for="(board,index) in BoardData" class="cell bg-gray-300 border border-gray-400 p-4" v-text="board"
                :class="{'bg-green-500':board.isSelected}" @click="select(index)"></button>
      </div>
  </div>
      <br>
      <div class="flex justify-center">
        <button class="bg-blue-500 hover:bg-blue-700 text-white font-bold py-2 px-4 rounded" @click="generateBoard(this.selectedlLevel)">Reset</button>
        <button class="bg-blue-500 hover:bg-blue-700 text-white font-bold py-2 px-4 rounded"@click="this.selectedlLevel=32, generateBoard(this.selectedlLevel)">Reset</button>
        <button class="bg-blue-500 hover:bg-blue-700 text-white font-bold py-2 px-4 rounded">Reset</button>

    </div>
  </div>


</template>

<style scoped>

</style>
