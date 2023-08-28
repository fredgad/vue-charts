<template>
  <div id="wrapper">
    <h3>Random charts</h3>
    <input
      class="coolButton"
      type="button"
      v-bind:value="`${props.stopped ? 'Start' : 'Stop'}`"
      @click="add"
    />

    <svg
      id="cont"
      @mousemove="checkPosition"
      @mouseup="dragStop"
      @mouseleave="dragStop"
    >
      <path
        :d="props.computedPath"
        fill="rgba(0,0,0,.1)"
        stroke="green"
        stroke-width="2"
      ></path>
      <circle
        class="point"
        v-for="(point, i) in props.randomsesSums"
        :key="i"
        :cy="point * 4 + 300"
        :cx="i * props.roadHeight"
        r="12"
        fill="rgba(0,0,0,.0)"
        @mousedown="dragStart(i)"
      ></circle>
    </svg>

    <input
      class="rng__height"
      type="range"
      @input="rngHeight"
      :value="rngRoadHeight"
      step=".01"
      min=".1"
      max="50"
    />
    <input
      class="rng__width"
      type="range"
      @input="rngWidth"
      :value="rngRoadWidth"
      step=".005"
      min=".01"
      max="3"
    />
    <div id="out">{{ mousePosY }} : {{ mousePosX }}</div>
  </div>
</template>

<script>
export default {
  name: "RandomProgress",
  props: ["props"],
  data() {
    return {
      rngRoadHeight: 5,
      rngRoadWidth: 1,
    };
  },
  computed: {
    calcPath() {
      this.$emit("calcPath");
    },
  },
  methods: {
    rngHeight(event) {
      this.rngRoadHeight = parseFloat(event.target.value);
      this.$emit("rngHeight", this.rngRoadHeight);
    },
    rngWidth(event) {
      this.rngRoadWidth = parseFloat(event.target.value);
      this.$emit("rngWidth", this.rngRoadWidth);
    },
    add() {
      this.$emit("add", 1);
    },
    checkPosition(e) {
      this.$emit("checkPosition", e);
    },
    dragStart(i) {
      this.$emit("dragStart", i);
    },
    dragStop() {
      this.$emit("dragStop");
    },
  },
};
</script>

<style scoped lang="scss">
#wrapper {
  position: relative;
  background: #eee;
  height: 50dvh;
  width: 96dvw;
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
    font-size: 22px;
    font-weight: bold;
  }
  .rng__height {
    position: relative;
    top: 20px;
    min-width: 300px;
    width: 70vw;
  }
  .rng__width {
    position: relative;
    top: 40px;
    min-width: 300px;
    width: 70vw;
  }

  .table {
    position: absolute;
  }
  #cont {
    display: flex;
    position: relative;
    height: 100%;
    top: 0;
    left: 0;
    min-width: 300px;
    width: 100%;
    // transition: 2s;

    // .point:hover {
    //   fill: red;
    // }
  }
}
</style>
