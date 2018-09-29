<template>
  <div id="app">
    <app-nav></app-nav>
    <div class="container text-center">
      <div class="even-better-container">
        <div id="plot-target"></div>
        <app-input-container :on-updated="update" :functions="functions"></app-input-container>
      </div>
    </div>
  </div>
</template>

<script>
import Nav from "./components/misc/Nav.vue";
import InputContainer from "./components/input/InputContainer.vue";
import plotFunctions from "function-plot";

export default {
  name: "app",
  data() {
    return {
      functions: []
    };
  },
  mounted() {
    this.functions.push({ fn: "" });
    this.update();
  },
  methods: {
    update() {    
      let options = { grid: true };
      let plotData = {
        target: "#plot-target",
        data: this.functions,
        width: 700,
        height: 700
      };
      Object.assign(plotData, options);
      plotFunctions(plotData);
    }
  },
  components: {
    AppNav: Nav,
    AppInputContainer: InputContainer
  }
};
</script>

<style>
div.even-better-container {
  display: flex;
  flex-flow: row;
}
div.input-group {
  margin: 50px auto;
}
</style>
