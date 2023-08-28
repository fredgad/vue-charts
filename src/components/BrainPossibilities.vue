<template>
  <div id="wrapper">
    <h1>
      Age-related <br />
      brain characteristics
    </h1>
    <div class="reac brain">Reaction</div>
    <div class="fast brain">Fast memory</div>
    <div class="slow brain">Slow memory</div>
    <div class="emp brain">Empathy</div>
    <div class="crys brain">Crystallized memory</div>
    <svg id="cont">
      <polygon
        :points="props.polyPath"
        fill="rgb(235,166,195)"
        stroke="rgb(12,48,110)"
        stroke-width="4"
      />

      <line x1="80" y1="0" x2="200" y2="200" stroke="black" stroke-width="2" />
      <line x1="320" y1="0" x2="200" y2="200" stroke="black" stroke-width="2" />
      <line
        x1="400"
        y1="220"
        x2="200"
        y2="200"
        stroke="black"
        stroke-width="2"
      />
      <line
        x1="200"
        y1="400"
        x2="200"
        y2="200"
        stroke="black"
        stroke-width="2"
      />
      <line x1="0" y1="220" x2="200" y2="200" stroke="black" stroke-width="2" />

      <circle cx="200" cy="200" r="6"></circle>
    </svg>
    <div id="img"></div>
    <div class="ages">{{ props.ages }}</div>
    <input
      id="rng"
      type="range"
      :value="props.ages"
      min="18"
      max="65"
      step="1"
      @input="rngChange"
    />
  </div>
</template>

<script>
export default {
  name: "BrainPossibilities",
  props: ["props"],
  data() {
    return {
      posFromScript: "44% 45%",
    };
  },
  methods: {
    rngChange() {
      this.$emit("rngChange", rng.value);
      this.recalculatePos;
    },
    inpChange() {
      if (inp.value > 65) {
        inp.value = 65;
      }
      this.$emit("rngChange", inp.value);
    },
  },
  computed: {
    recalculatePos() {
      let pos = 44;
      console.log(this.props.ages, "ages");

      if (this.props.ages > 24) {
        pos = 60;
      }
      if (this.props.ages > 40) {
        pos = 76;
      }
      if (this.props.ages > 59) {
        pos = 93;
      }
      console.log(pos, "pos");
      this.posFromScript = `${pos}% 45%`;

      return this.posFromScript;
    },
  },
};
</script>

<style lang="scss" scoped>
#wrapper {
  position: relative;
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  height: 100%;
  min-height: 700px;
  margin-bottom: 80px;

  #cont {
    position: relative;
    width: 95vw;
    max-width: 400px;
    height: 400px;
    min-height: 400px;
  }
  h1 {
    padding-bottom: 35px;
    line-height: 30px;
    text-align: center;
  }
  #img {
    background: url("../assets/ages.jpg");
    height: 180px;
    min-height: 180px;
    width: 65px;
    margin-top: 15px;
    background-position: v-bind("posFromScript");
    background-size: 800% 200%;
    background-repeat: no-repeat;
    transition: 0s;
  }
  .ages {
    font-size: 24px;
    margin-bottom: 10px;
  }
  .brain {
    position: absolute;
  }
  .reac {
    top: 315px;
    left: 0;
  }
  .fast {
    top: 70px;
    left: 35px;
  }
  .slow {
    top: 70px;
    right: 35px;
  }
  .emp {
    top: 370px;
    right: 0;
  }
  .crys {
    top: 490px;
  }
  input[type="range"] {
  }

  @media screen and (max-width: 402px) {
    #cont {
      transform: scale(0.7);
      overflow: visible;
    }
    .fast {
      top: 125px;
      left: 45px;
    }
    .slow {
      top: 125px;
      right: 0;
    }
    .crys {
      top: 440px;
    }
    .emp {
      top: 378px;
    }
  }
}
</style>
