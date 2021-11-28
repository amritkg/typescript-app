<template>
  <div id="head">
    <Tab />
    <Drop />
  </div>
</template>

<script lang="ts">
import { Options, Vue } from "vue-class-component";
import Drop from "@/components/Drop.vue";
import Drag from "@/components/Drag.vue";
import Tab from "@/components/Tab.vue";
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
    Tab,
  },
})
export default class Home extends Vue {}
</script>
<style>
</style>