<template>
  <div id="head">
    <div id="butDiv"></div>
    <div id="mainDiv">
      <Drag :id="toPass" />
    </div>
    <Drop />
  </div>
</template>

<script lang="ts">
import { Options, Vue } from "vue-class-component";
import Drop from "@/components/Drop.vue";
import Drag from "@/components/Drag.vue";
var head: HTMLElement;
var butDiv: HTMLElement;
var grA: HTMLElement;
var grB: HTMLElement;
var grC: HTMLElement;
var mainDiv: HTMLElement;
var dA: HTMLElement;
var dB: HTMLElement;
var dC: HTMLElement;
var dragged = "";
document.addEventListener("dragstart", function (event) {
  const k = event.target as Element;
  if (
    k.nodeName == "IMG" &&
    k.parentElement!.style.backgroundColor == "orange"
  ) {
    dragged = k.id;
  } else {
    dragged = "";
  }
});
document.addEventListener("dragover", function (event) {
  event.preventDefault();
});
document.addEventListener("drop", async function (event) {
  var droploc = event.target as Element;
  if (dragged != "") {
    if (droploc.nodeName == "DIV" && droploc.getAttribute("class") == "zone") {
      droploc.innerHTML = "";
      var tempD = dragged;
      var test = document.getElementById(tempD)!.cloneNode();
      droploc.appendChild(test);
      await delay(5000);
      var counter = 0;
      for (counter = 0; counter < droploc.children.length; counter++) {
        if (test == droploc.children[counter]) {
          droploc.removeChild(droploc.children[counter]);
        }
      }
    } else if (
      droploc.nodeName == "IMG" &&
      droploc.parentElement!.getAttribute("class") == "zone"
    ) {
      const idS = droploc.parentElement!.getAttribute("id")!;
      var par = document.getElementById(idS)!;
      par.innerHTML = "";
      var tempE = dragged;
      var testx = document.getElementById(tempE)!.cloneNode();
      par.appendChild(testx);
      await delay(5000);
      for (counter = 0; counter < par.children.length; counter++) {
        if (testx == par.children[counter]) {
          par.removeChild(par.children[counter]);
        }
      }
    }
  }
});

function delay(ms: number) {
  return new Promise((resolve) => setTimeout(resolve, ms));
}
@Options({
  components: {
    Drag,
    Drop,
  },
})
export default class Home extends Vue {
  toPass!: number;
  isUpdating!: boolean;
  data() {
    return {
      toPass: 0,
      isUpdating: false,
    };
  }
  mounted() {
    head = document.getElementById("head")!;
    butDiv = document.getElementById("butDiv")!;
    mainDiv = document.getElementById("mainDiv")!;
    //buttons
    grA = document.createElement("button");
    grB = document.createElement("button");
    grC = document.createElement("button");
    butDiv.style.display = "inline-block";
    grA.textContent = "group_a";
    grB.textContent = "group_b";
    grC.textContent = "group_c";
    grA.addEventListener("click", this.aClick);
    grB.addEventListener("click", this.bClick);
    grC.addEventListener("click", this.cClick);
    butDiv.appendChild(grA);
    butDiv.appendChild(grB);
    butDiv.appendChild(grC);
    //button styles
    //rounded corners
    grA.style.borderRadius = "7px 7px 0px 0px";
    grB.style.borderRadius = "7px 7px 0px 0px";
    grC.style.borderRadius = "7px 7px 0px 0px";
    grA.style.paddingLeft = "12px";
    grA.style.paddingRight = "12px";
    grB.style.paddingLeft = "12px";
    grB.style.paddingRight = "12px";
    grC.style.paddingLeft = "12px";
    grC.style.paddingRight = "12px";
    //borders
    const borS = "1px solid";
    grA.style.borderLeft = borS;
    grA.style.borderRight = borS;
    grA.style.borderTop = borS;
    grB.style.borderLeft = borS;
    grB.style.borderRight = borS;
    grB.style.borderTop = borS;
    grC.style.borderLeft = borS;
    grC.style.borderRight = borS;
    grC.style.borderTop = borS;
  }
  aClick(): void {
    this.toPass = 0;
    grA.style.backgroundColor = "inherit";
    grA.style.borderBottom = "1px solid white";
  }
  bClick(): void {
    this.toPass = 1;
    grB.style.backgroundColor = "inherit";
    grB.style.borderBottom = "1px solid white";
  }
  cClick(): void {
    this.toPass = 2;
    grC.style.backgroundColor = "inherit";
    grC.style.borderBottom = "1px solid white";
  }
  removeAll(): void {
    grA.style.backgroundColor = "lightgray";
    grB.style.backgroundColor = "lightgray";
    grC.style.backgroundColor = "lightgray";
    grA.style.borderBottom = "1px solid black";
    grB.style.borderBottom = "1px solid black";
    grC.style.borderBottom = "1px solid black";
  }
}
</script>
<style>
</style>