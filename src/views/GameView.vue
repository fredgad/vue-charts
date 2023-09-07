<template>
  <div>
    <Menu
      v-if="win"
      :props="{ array, timer, steps, startGame, firstStart, firstStartCheck }"
    />
    <Game v-else :props="{ array, timer, steps, startGame, makeStep }" />
  </div>
</template>

<script>
import Game from "../components/game/Game.vue";
import Menu from "../components/game/Menu.vue";

export default {
  name: "game-view",
  components: {
    Game,
    Menu,
  },
  data() {
    return {
      invis: 15,
      array: [0, 1, 2, 3, 4, 5, 6, 7, 8, 9, 10, 11, 12, 13, 14, 15],
      timer: 0,
      steps: 0,
      win: true,
      firstStartCheck: true,
      timerCheck: true,
    };
  },
  methods: {
    firstStart() {
      this.firstStartCheck = false;
      this.startGame();
      this.timerStart();
    },
    startGame() {
      this.win = false;
      (this.array = [0, 1, 2, 3, 4, 5, 6, 7, 8, 9, 10, 11, 12, 13, 14]),
        (this.steps = 0);
      this.timer = 0;
      this.timerCheck = true;

      this.generateSolvableState();
    },
    generateSolvableState() {
      this.shuffleArray();

      // Check if the permutation is even; if not, swap two elements
      if (!this.isEvenPermutation(this.array)) {
        // Find two elements to swap such that it becomes an even permutation
        for (let i = 0; i < this.array.length - 1; i++) {
          for (let j = i + 1; j < this.array.length; j++) {
            if (this.array[i] > this.array[j]) {
              // Swap the elements
              [this.array[i], this.array[j]] = [this.array[j], this.array[i]];
              break;
            }
          }
          if (this.isEvenPermutation(this.array)) {
            break;
          }
        }
      }

      // Add the empty space (15) to the last position
      this.array.push(15);
      console.log(this.array);
    },
    isEvenPermutation(numbers) {
      let inversions = 0;
      for (let i = 0; i < numbers.length - 1; i++) {
        for (let j = i + 1; j < numbers.length; j++) {
          if (numbers[i] > numbers[j]) {
            inversions++;
          }
        }
      }
      return inversions % 2 === 0;
    },
    shuffleArray() {
      for (let i = this.array.length - 1; i > 0; i--) {
        const j = Math.floor(Math.random() * (i + 1));
        [this.array[i], this.array[j]] = [this.array[j], this.array[i]];
      }
    },
    makeStep() {
      let target = event.target.getAttribute("data-key"),
        targetPos = this.array.indexOf(+target),
        invisPos = this.array.indexOf(this.invis);

      if (
        targetPos === invisPos + 1 ||
        targetPos === invisPos - 1 || // Gorizontal check
        targetPos === invisPos + 4 ||
        targetPos === invisPos - 4
      ) {
        // Vertical check
        let pos1 = this.array.splice(targetPos, 1, this.array[invisPos]);
        this.array[invisPos] = pos1[0];
        this.steps++;
        this.winCheck();
      }
    },
    winCheck() {
      // Проверка на победу
      const winGame = this.array.every((el, i) => el === i);
      if (winGame) {
        // Если победа
        this.win = true;
        this.timerCheck = false;
      }
    },
    timerStart() {
      // Запуск таймера
      const time = setInterval(() => {
        if (this.timerCheck) {
          this.timer++;
        }
      }, 1e3);
    },
  },
};
</script>
