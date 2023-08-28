<template>
  <div class="about">
    <RandomProgress
      v-on:add="addSome"
      v-on:rngHeight="rngHeight"
      v-on:rngWidth="rngWidth"
      v-on:checkPosition="checkPosition"
      v-on:dragStart="dragStart"
      v-on:dragStop="dragStop"
      :props="{
        randomses,
        randomsesSums,
        roadHeight,
        roadWidth,
        mousePosX,
        mousePosY,
        addSome,
        computedPath,
        stopped,
      }"
    />
  </div>
</template>

<script>
import RandomProgress from "../components/RandomProgress.vue";
// import { setInterval } from "timers";

export default {
  name: "about",
  components: {
    RandomProgress,
  },
  data() {
    return {
      randomses: [0],
      randomsesSums: [0],
      roadHeight: 3,
      roadWidth: 0.5,
      computedPath: "M0 200",
      mousePosX: 0,
      mousePosY: 0,
      mouseCheck: false,
      choosenPoint: 0,
      stopped: true,
    };
  },
  computed: {
    calcPath() {
      let path = "M0 200";
      for (let x = 0; x < this.randomses.length; x++) {
        path += ` L ${x * this.roadHeight} ${
          this.roadWidth * this.randomsesSums[x] * 4 + 200
        }`;
      }
      this.computedPath = path;
      console.log(this.randomsesSums + "from calc");
    },
  },
  methods: {
    // // addSome(x) {
    // //   for (; x; x--) {
    // //     var newRandom = Math.floor(Math.random() * 11 - 5);
    // //     this.randomses.push(newRandom)

    // //     var newPoint = this.countSum(this.randomses)
    // //     this.randomsesSums.push(newPoint)
    // //   }
    // //   this.calcPath
    // // },
    startInterval() {
      window.setInterval(() => {
        if (!this.stopped) {
          var newRandom = Math.floor(Math.random() * 11 - 5);
          this.randomses.push(newRandom);

          var newPoint = this.countSum(this.randomses);
          this.randomsesSums.push(newPoint);

          this.calcPath;
        }
      }, 35);
    },
    addSome(x) {
      this.stopped = !this.stopped;
    },
    countSum() {
      let currentDifference = 0;
      for (let x = 0; x < this.randomses.length; x++) {
        currentDifference += +this.randomses[x];
      }
      return currentDifference;
    },
    rngHeight(rngValue) {
      this.roadHeight = rngValue;
      this.calcPath;
    },
    rngWidth(rngValue) {
      this.roadWidth = rngValue;
      this.calcPath;
    },
    dragStart(i) {
      this.mouseCheck = true;
      // document.querySelectorAll('.point')[i].style.fill = 'green';
      this.choosenPoint = i;
      console.log(this.choosenPoint);
    },
    dragMove() {
      console.log(this.randomsesSums + "from move");
      if (this.mouseCheck) {
        this.randomsesSums[this.choosenPoint] = (this.mousePosY - 300) / 4;
        // this.addSome(1)
      }
    },
    checkPosition(e) {
      var rect = wrapper.getBoundingClientRect();
      this.mousePosX = e.clientX - rect.left;
      this.mousePosY = e.clientY - rect.top;
      this.dragMove();
    },
    dragStop() {
      this.mouseCheck = false;
    },
  },
  beforeMount() {
    this.startInterval();
  },
};
</script>

<style></style>
