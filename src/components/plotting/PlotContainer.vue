<template>
  <div class="plots">
    <app-plot v-for="plot in plots" :plotData="plot.functions" :plotID="plot.id" :options="options" :key="plot.id"></app-plot>
  </div>
</template>

<script>
import Plot from "./Plot";

export default {
  name: "PlotContainer",
  props: {
    plots: {
      type: Array,
      required: true
    },
    options: {
      type: Object,
      default: () => {},
      required: false
    }
  },

  components: {
    AppPlot: Plot
  }
};
</script>

<style>
</style>
