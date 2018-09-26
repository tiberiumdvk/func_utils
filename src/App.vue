<template>
  <div id="app">
    <app-nav></app-nav>
    <div class="container text-center">
      <div class="input-group w-75">
        <div class="input-group-prepend">
          <span class="input-group-text">&#402;&#x27EE;&#x1d465;&#x27EF; &#61;</span>
        </div>
        <input type="text" class="form-control" placeholder="x^2" v-model.trim="newPlot" @blur="history.position = -1" @keydown.up="loadFormula(1)" @keydown.down="loadFormula(-1)" @keyup.enter="addPlot">
      </div>

      <app-plot-container :plots="plots" :options="{grid: true,}"></app-plot-container>
    </div>
  </div>
</template>

<script>
import Nav from "./components/misc/Nav.vue";
import PlotContainer from "./components/plotting/PlotContainer.vue";

export default {
  name: "app",
  data() {
    return {
      newPlot: "",
      plots: [],
      history: {
        position: -1,
        plots: []
      }
    };
  },
  methods: {
    generateID() {
      return (
        "plot_" +
        Math.random()
          .toString(36)
          .substr(2, 6)
      );
    },

    addPlot() {
      this.plots.unshift({
        id: this.generateID(),
        functions: [{ fn: this.newPlot }]
      });

      this.history.plots.unshift(this.newPlot);
      this.history.position = -1;
      this.newPlot = "";
    },

    loadFormula(change) {
      let newPosition = this.history.position + change;

      if (newPosition >= this.history.plots.length) {
        return;
      }

      if (newPosition < 0) {
        this.newPlot = "";
      }

      this.history.position = newPosition;
      this.newPlot = this.history.plots[newPosition];
    }
  },
  components: {
    AppNav: Nav,
    AppPlotContainer: PlotContainer
  }
};
</script>

<style>
div.input-group {
  margin: 50px auto;
}
</style>
