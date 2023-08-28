<template>
  <div id="wrapper">
    <div id="cont">
      <div id="box"></div>
    </div>
    <div id="scrollBar">
      <div id="scrollLine"></div>
    </div>
  </div>
</template>
 
<script>
export default {
  name: 'scrollBar'
}
</script>

<style lang="scss" scoped>
#wrapper {
  display: grid;
  grid-template-columns: 1fr;
  justify-items: center;
  align-items: center;
  min-height: 700px;

  #cont {
    position: relative;
    height: 400px;
    width: 800px;
    border: 2px solid red;
    display: flex;
    justify-content: center;
    align-items: center;

    #box {
      position: absolute;
    }
  }

  #scrollBar {
    position: relative;
    height: 30px;
    width: 1200px;
    background: orange;

    #scrollLine {
      position: absolute;
      background: #444;
      top: 0;
      height: 30px;
      min-width: 30px;
    }
  }
}


</style>