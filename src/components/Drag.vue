<template>
  <div
    id="drag"
    style="background-color: orange; border: 1px solid black; padding: 5px"
  ></div>
</template>
<script lang="ts">
import { Options, Vue } from "vue-class-component";
var length = [11,6,8];
var letter = ["a","b","c"];
@Options({
  props: {
    id: Number,
  },
})
export default class Drag extends Vue {
  id!: number;
  mounted() {
    console.log(this.id);
    const drag = document.getElementById("drag")!;
    drag.draggable = false;
    var i = 0;
    for (i = 1; i < length[this.id]; i++) {  
      const im = document.createElement("img");
      im.style.padding = "2px";
      im.src = require("../assets/group_"+letter[this.id]+"/"+letter[this.id]+"-" + i + ".png");
      console.log(im.src);
      im.setAttribute("id", letter[this.id] + i);
      im.style.width = "90px";
      im.style.height = "relative";
      im.draggable = true;
      drag.appendChild(im);
    }
  }
}
</script>
<style>
</style>