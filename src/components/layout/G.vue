<template>
  <div id="wrapper" @mousemove="checkPosition">
    <input type="button" value="Жми!" @click="addSome">
    <!-- <div class="table" v-for="rand,index in randomses">{{ randomsesSums[index] }} : {{ rand }}</div> -->

    <svg id="cont" :style="`width: ${randomses.length * roadSize}px`">
      <path :d="calcPath" fill="rgba(0,0,0,.1)" stroke="green" stroke-width="2"></path>
      <circle
        class="point"
        v-for="point,i in randomsesSums"
        :key="i"
        :cy="point*4 + 300"
        :cx="i*roadSize"
        r="6"
        fill="orange"
        @click="dragPoint(i)"
      ></circle>
    </svg>
    <!-- :style="`top: ${point*4 + 200}px;left: ${i*20}px;transform: scaleX(${1/roadSize })`"> -->
    <!-- <input type="range" v-model:value="roadSize" step=".01" min="0.01" max="1"> -->
    <input class="rng__size" type="range" v-model:value="roadSize" step=".01" min=".1" max="50">
    <input class="rng__width" type="range" v-model:value="roadWidth" step=".01" min=".1" max="10">
    <div id="out">{{ roadSize }} : {{ mousePosY }}</div>
  </div>
</template>

<script>
export default {
  name: "RandomProgress",
  data() {
    return {
      randomses: [0],
      randomsesSums: [0],
      roadSize: 10,
      roadWidth: 5,
      mousePosX: 0,
      mousePosY: 0
    };
  },
  computed: {
    calcPath() {
      let path = "M0 200";
      for (let x = 0; x < this.randomses.length; x++) {
        path += ` L ${x * this.roadSize} ${this.roadWidth *
          this.randomsesSums[x] *
          4 +
          300}`;
      }
      return path;
    }
  },
  methods: {
    addSome() {
      for (let x = 9; x; x--) {
        var newRandom = Math.floor(Math.random() * 11 - 5);
        this.randomses.push(newRandom);

        var newPoint = this.countSum(this.randomses);
        this.randomsesSums.push(newPoint);
      }
    },
    countSum() {
      let currentDifference = 0;
      for (let x = 0; x < this.randomses.length; x++) {
        currentDifference += +this.randomses[x];
      }
      return currentDifference;
    },
    squize() {
      cont.style.transform = "scaleX(.4)";
    },
    dragPoint(i) {
      console.log(i);
      document.querySelectorAll('.point')[i].style.fill = 'black';
      
    },
    checkPosition(e) {
      var rect = wrapper.getBoundingClientRect();
      this.mousePosX =  e.clientX - rect.left;
      this.mousePosY =  e.clientY - rect.top;
    }
  }
};
</script>

<style scoped lang="scss">
#wrapper {
  position: relative;
  background: #eee;
  height: 600px;
  width: 100vw;
  margin-top: 30px;
  text-align: center;

  #out {
    position: absolute;
    top: 100%;
    left: 49vw;
    width: 30px;
  }
  input[type="button"] {
    position: absolute;
    top: -24px;
  }
  .rng__size {
    position: relative;
    top: 100px;
    width: 1000px;
  }
  .rng__width {
    position: relative;
    top: 100px;
    width: 1000px;
  }

  .table {
    position: absolute;
  }
  #cont {
    display: flex;
    position: relative;
    border: 2px solid red;
    height: 100%;
    top: 0;
    left: 0;
    min-width: 100vw !important;
    // transition: 2s;

    .point:hover {
      fill: red;
    }
  }
}
</style>
