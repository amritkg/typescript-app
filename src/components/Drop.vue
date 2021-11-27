<template>
  <div id="drop">
    <div id="holder" style="display: stretch"></div>
  </div>
</template>
<script lang="ts">
import { Options, Vue } from "vue-class-component";
export default class Drop extends Vue {
  mounted() {
    const drop = document.getElementById("drop")!;
    const holder = document.getElementById("holder")!;
    var j = 0;
    var i = 0;
    for (i = 0; i < 11; i++) {
      const horDivGrid = document.createElement("div");
      holder.appendChild(horDivGrid);
      horDivGrid.setAttribute("id", i + "");
      horDivGrid.style.alignContent = "center";
      for (j = 0; j < 11; j++) {
        const verGrid = document.createElement("div");
        verGrid.style.display = "table-cell";
        // verGrid.style.border = "1px solid lightgray";
        // verGrid.textContent = j + "-" + i;
        horDivGrid.appendChild(verGrid);
        if ((j == 1 && i == 6) || (j == 5 && i == 8) || (j == 7 && i == 5)) {
          verGrid.style.backgroundColor = "green";
          verGrid.style.width = "91px";
          verGrid.style.height = "161px";
          verGrid.setAttribute("class", "zone");
          verGrid.setAttribute("id", "" + j + i);
        } else {
          verGrid.style.width = "91px";
          verGrid.style.height = "32px";
        }
      }
    }
  }
}
</script>
<style></style>