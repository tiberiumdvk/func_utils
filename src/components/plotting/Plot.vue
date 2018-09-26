<template>
  <div :id="plotID" class="plot"></div>
</template>

<script>
import functionPlot from "function-plot";

export default {
  name: "Plot",
  props: {
    plotData: {
      type: Array,
      required: true
    },
    plotID: {
      type: String,
      required: true
    },
    options: {
      type: Object,
      default: () => {},
      required: false
    }
  },

  mounted() {
    const containerWidth = this.$el.parentElement.offsetWidth;
    let width, height;

    // This is not as responsive however there's not much
    // flexibility when working with bloody canvases

    // Bootstrap threshold
    if (containerWidth < 930) {
      width = containerWidth;
      height = containerWidth * 0.64;
    } else {
      width = containerWidth * 0.85;
      height = containerWidth * 0.51;
    }

    const plot = {
      target: "#" + this.plotID,
      data: this.plotData,
      width,
      height
    };
    Object.assign(plot, this.options);

    functionPlot(plot);
  }
};
</script>

<style>
div.plot {
  margin: 50px 5px;
}

div.plot > svg > text {
  transform: translateY(1%);
}
</style>
