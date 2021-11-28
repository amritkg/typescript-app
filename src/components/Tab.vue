<template>
  <div class="container">
    <div class="tabs">
      <a
        class="stack-top"
        v-on:click="activetab = 0"
        v-bind:class="[activetab === 0 ? 'active' : '']"
        >group_a</a
      >
      <a
        class="stack-mid"
        v-on:click="activetab = 1"
        v-bind:class="[activetab === 1 ? 'active' : '']"
        >group_b</a
      >
      <a
        v-on:click="activetab = 2"
        v-bind:class="[activetab === 2 ? 'active' : '']"
        >group_c</a
      >
    </div>

    <div class="content">
      <div class="tabcontent"><Drag :tabid="activetab" /></div>
    </div>
  </div>
</template>

<script lang = "ts">
import { Options, Vue } from "vue-class-component";
import Drag from "@/components/Drag.vue";
@Options({
  components: {
    Drag,
  },
})
export default class Tab extends Vue {
  activetab!: number;
  data() {
    return {
      activetab: 0,
    };
  }
}
</script>

<style>
.container {
  margin: 20px 20px 0px 20px;
  font-family: Arial, Helvetica, sans-serif;
  font-size: 0.9em;
  color: #888;
  background-color: #fff;
}

.tabs {
  overflow: hidden;
  margin-left: 0px;
  margin-bottom: -1px;
}

.tabs a {
  float: left;
  cursor: pointer;
  padding: 8px 16px;
  transition: background-color 0.2s;
  transition: color 0.2s;
  border: 1px solid #000;
  background-color: #f1f1f1;
  border-radius: 10px 10px 0 0;
  font-weight: bold;
  overflow: visible;
  position: relative;
  margin-right: -15px;
}
.tabs a:last-child {
  border-radius: 0px 10px 0px 0px;
  padding-left: 35px;
}
.tabs a:nth-child(2) {
  border-radius: 0px 10px 0px 0px;
  padding-left: 35px;
}
.stack-top {
  z-index: 9;
}
.stack-mid {
  z-index: 8;
}

.tabs a:hover {
  background-color: #aaa;
  color: #fff;
}

.tabs a.active {
  background-color: #fff;
  color: #484848;
  border-bottom: 1px solid #fff;
  cursor: default;
}

.tabcontent {
  padding: 30px;
  border: 1px solid #000;
}
</style>

