<template>
  <div id="home">
    <BrainPossibilities
      v-on:rngChange="rngChange"
      :props="{
        ages,
        reaction,
        fastMemory,
        empathy,
        slowMemory,
        crystalized,
        polyPath,
      }"
    />
  </div>
</template>

<script>
import BrainPossibilities from "../components/BrainPossibilities.vue";

export default {
  name: "home",
  components: {
    BrainPossibilities,
  },
  data() {
    return {
      ages: 18,
      reaction: 100,
      fastMemory: [],
      empathy: [45],
      slowMemory: [
        65, 70, 75, 80, 85, 90, 95, 100, 100, 100, 100, 100, 100, 100, 100, 100,
        100, 98, 96, 94, 92, 90, 88, 86, 84, 82, 80, 78, 76, 74, 72, 70, 68, 66,
        64, 62, 60, 58, 56, 54, 52, 50, 48, 46, 44, 42, 41, 40,
      ],
      crystalized: 15,
      polyPath: "80,0 278,70 277,208 200,220 0,220",
    };
  },
  methods: {
    rngChange(val) {
      this.ages = val;
      this.recalculate;
    },
    calcFastMemory2() {
      if (this.ages < 25) {
        return 0;
      } else {
        return 0 + (200 / 47) * (this.ages - 25);
      }
    },
    calcFastMemory1() {
      if (this.ages < 25) {
        return 80;
      } else {
        return 80 + (120 / 47) * (this.ages - 25);
      }
    },
    calcEmpathy1() {
      if (this.ages > 46) {
        return 400;
      } else {
        return 200 + (200 / 47) * this.ages;
      }
    },
    calcEmpathy2() {
      if (this.ages > 46) {
        return 220;
      } else {
        return 200 + (20 / 47) * this.ages;
      }
    },
  },
  computed: {
    recalculate() {
      this.polyPath = `
          ${this.calcFastMemory1()},
          ${this.calcFastMemory2()}
          ${200 + 120 * (this.slowMemory[this.ages - 18] / 100)},${
        (200 * (100 - this.slowMemory[this.ages - 18])) / 100
      }
          ${this.calcEmpathy1()},${this.calcEmpathy2()}
          200,${220 + (180 / 47) * (this.ages - 18)}
          ${(200 / 47) * (this.ages - 18)},${
        220 - (20 / 47) * (this.ages - 18)
      }`;

      return this.polyPath;
    },
  },
};
</script>

<style lang="scss">
#home {
  padding-top: 70px;
}
</style>
