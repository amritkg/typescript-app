<template>
  <div
    id="drag"
    style="background-color: orange; border: 1px solid black; padding: 5px"
    align = "left"
  ></div>
</template>
<script lang="ts">
import { Options, Vue } from "vue-class-component";
import { Watch } from "vue-property-decorator";
var length = [11, 6, 8];
var letter = ["a", "b", "c"];
@Options({
  props: {
    tabid: Number,
  },
})
export default class Drag extends Vue {
  tabid!: number;
  mounted() {
      this.starter();
  }
  @Watch("tabid")
  starter(): void {
    const drag = document.getElementById("drag")!;
    drag.innerHTML = "";
    drag.draggable = false;
    var i = 0;
    for (i = 1; i < length[this.tabid]; i++) {
      const im = document.createElement("img");
      im.src = require("../assets/group_" +
        letter[this.tabid] +
        "/" +
        letter[this.tabid] +
        "-" +
        i +
        ".png");
      im.setAttribute("id", letter[this.tabid] + i);
      im.setAttribute("class", "im");
      im.draggable = true;
      drag.appendChild(im);
    }
  }
}
</script>
<style>
.im{
    width: 90px;
    height: relative;
    padding: 5px;
}
</style>