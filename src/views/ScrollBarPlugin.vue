<template>
  <div id="scroll">
    <ScrollBar />
  </div>
</template>

<script>
import ScrollBar from "../components/ScrollBar.vue";

export default {
  name: "ScrollBarPlugin",
  components: {
    ScrollBar,
  },
  data() {
    return {
      scrollLinePos: 0,
    };
  },
};
if (document.getElementById("scrollBar")) {
  var scrollBar = document.querySelector("#scrollBar"),
    scrollLine = document.querySelector("#scrollLine"),
    likedCont = document.querySelector("#compare-products-slider"),
    likedBox = document.querySelector(
      "#compare-products-slider .compare-products-list-slider"
    );

  var dragCheck = false;
  (dragPos = 0), (downPos = 0);

  //Set the box width
  likedBox.style.width = likedBox.children.length * 265 + "px";

  if (likedBox.offsetWidth > likedCont.offsetWidth) {
    scrollLine.style.width =
      scrollBar.offsetWidth / (likedBox.offsetWidth / likedCont.offsetWidth) +
      "px";
  } else {
    scrollLine.style.width = "100%";
  }

  scrollLine.addEventListener("mousedown", (e) => {
    dragCheck = true;
    downPos = e.clientX - scrollLine.getBoundingClientRect().left;
  });
  document.addEventListener("mousemove", (e) => {
    if (dragCheck) {
      if (
        e.clientX - downPos + 12 > scrollBar.offsetLeft &&
        e.clientX + 12 - downPos + scrollLine.offsetWidth <
          scrollBar.offsetLeft + scrollBar.offsetWidth
      ) {
        var scale = scrollBar.offsetWidth - scrollLine.offsetWidth;
        var posX = e.clientX - downPos - scrollBar.offsetLeft;
        var translateX = (posX / scale) * (likedBox.offsetWidth - 1000);

        scrollLine.style.transform = `translate(${posX}px)`;
        likedBox.style.transform = `translate(-${translateX}px)`;
      }
    }
  });
  document.addEventListener("mouseup", (e) => {
    dragCheck = false;
  });
  document.addEventListener("mouseleave", (e) => {
    dragCheck = false;
  });

  let deleteElemment = document.querySelectorAll(".btn_icon_delete");
  for (let x = 0; x < deleteElemment.length; x++) {
    deleteElemment[x].addEventListener("click", () => {
      likedBox.style.width = (likedBox.children.length - 1) * 265 + "px";
      if (likedBox.offsetWidth > likedCont.offsetWidth) {
        scrollLine.style.width =
          scrollBar.offsetWidth /
            (likedBox.offsetWidth / likedCont.offsetWidth) +
          "px";
      } else {
        scrollLine.style.width = "100%";
      }
    });
  }
}
</script>

<style lang="scss"></style>
