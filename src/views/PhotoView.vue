<template>
  <div class="home">
    <PhotoGame
      :props="{ vertical, gorisontal, sideAmount, boxWidth, boxHeight }"
      v-on:changeAmount="changeAmount"
      v-on:mix="mix"
      v-on:animate="animate"
    />
  </div>
</template>

<script>
// @ is an alias to /src
import PhotoGame from "../components/PhotoGame.vue";
// import { setTimeout } from "timers";

export default {
  name: "Photo",
  components: {
    PhotoGame,
  },
  data() {
    return {
      vertical: 1,
      gorisontal: 1,
      sideAmount: [0],
      verticalPositions: [],
      gorisontalPositions: [],
      width: 500,
      height: 375,
      boxArray: [],
      boxWidth: 500,
      boxHeight: 375,
      aminationIterate: 0,
    };
  },
  methods: {
    changeAmount(ver, gor) {
      this.vertical = ver;
      this.gorisontal = gor;
      this.sideAmount = [];
      for (let x = 0; x < ver * gor; x++) {
        this.sideAmount.push(x);
      }

      this.cut();
    },
    cut() {
      cont.style.gridTemplateColumns = `repeat(${this.gorisontal}, 1fr)`;
      this.boxWidth = this.width / this.gorisontal;
      this.boxHeight = this.height / this.vertical;

      this.verticalPositions = [];
      this.gorisontalPositions = [];

      let ver = 100 / (this.vertical - 1);
      let gor = 100 / (this.gorisontal - 1);
      if (!(this.vertical - 1)) {
        ver = 0;
      }
      if (!(this.gorisontal - 1)) {
        gor = 0;
      }
      let verticalPudding = ver;
      let gorisontalPudding = gor;
      let gorisontalPos = 0;
      let verticalPos = 0;

      for (let x = 0; x < this.gorisontal * this.vertical; x++) {
        this.verticalPositions.push(verticalPos);
        this.gorisontalPositions.push(gorisontalPos);
        gorisontalPos += gorisontalPudding;

        if ((x + 1) % this.gorisontal == 0) {
          verticalPos += verticalPudding;
          gorisontalPos = 0;
        }
      }
      this.recaunt();
    },
    recaunt() {
      window.setTimeout(() => {
        for (let x = 0; x < cont.children.length; x++) {
          let dataPos = cont.children[x].getAttribute("data-pos");
          let dataX = this.verticalPositions[dataPos];
          let dataY =
            this.gorisontalPositions[
              +cont.children[x].getAttribute("data-pos")
            ];

          cont.children[x].style.backgroundPosition = `${dataY}% ${dataX}%`;
          cont.children[x].style.outline = "1px solid #fff";
        }
      }, 0);
    },
    animate() {
      for (let x = 0; x < cont.children.length; x++) {
        cont.children[x].style.animation = `animation${
          this.aminationIterate
        } 2s ease ${x / 100}s`;
        console.log(x);
      }
      this.aminationIterate++;
      if (this.aminationIterate > 2) {
        this.aminationIterate = 0;
      }
      window.setTimeout(() => {
        this.mix();
      }, 999);
    },
    net() {},
    mix() {
      this.sideAmount.sort(() => {
        return 0.5 - Math.random();
      });
      this.recaunt();
    },
    startDrag() {
      console.log("start");
    },
    continueDrag() {
      console.log("continue");
    },
    stopDrag() {
      console.log("stop");
    },
  },
};
</script>

<style>
@keyframes animation0 {
  0% {
    transform: rotate(0) translateZ(0px);
  }

  100% {
    transform: rotate(360deg) translateZ(-400px);
  }
}

@keyframes animation1 {
  0% {
    transform: rotate(0) translateZ(20px);
  }
  50% {
    transform: rotate(360deg) translateZ(-10000px);
  }
  100% {
    transform: rotate(360deg) translateZ(20px);
  }
}
@keyframes animation2 {
  0% {
    transform: rotate(0) translateZ(0px);
  }
  50% {
    transform: rotate(360deg) translateZ(-10000px);
  }
  100% {
    transform: rotate(360deg) translateZ(0px);
  }
}
</style>
