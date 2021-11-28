<template>
  <div id="holder" style="display: stretch"></div>
</template>
<script lang="ts">
import { Options, Vue } from "vue-class-component";
export default class Drop extends Vue {
  mounted() {
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
        horDivGrid.appendChild(verGrid);
        if ((j == 1 && i == 6) || (j == 5 && i == 8) || (j == 7 && i == 5)) {
          verGrid.setAttribute("class", "zone");
          verGrid.setAttribute("id", "" + j + i);
        } else {
          verGrid.setAttribute("class", "nozone");
        }
      }
    }
  }
}
</script>
<style>
.zone{
    background-color: #61d937;
    width: 91px;
    height: 161px;
}
.nozone{
    width:91px;
    height: 8px;
}
</style>