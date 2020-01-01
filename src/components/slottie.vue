<template>
  <div class="slottie-container">
    <div class="slottie-animation"></div>
  </div>
</template>

<script>
import * as lottie from "lottie-web";
import graph from "src/assets/data.json";

export default {
  name: "slottie",
  props: {
    x: Number,
    y: Number,
    z: Number
  },
  data: () => ({
    elt: null,
    animData: null,
    animAPI: null
  }),
  computed: {
    app() {
      return this.$root.$children[0];
    }
  },
  mounted() {
    this.elt = this.$el.children[0];
    console.log(this.x);
    this.init();
  },
  methods: {
    init() {
      // First initialize lottie as you would normally
      this.animData = this.buildAnimation();
      // Then pass your lottie.loadAnimation result into "lottie_api.createAnimationApi()":
      this.animAPI = lottie_api.createAnimationApi(this.animData);

      // This is how you control an Effects slider:
      let xSlider = this.animAPI.getKeyPath("graphValues,Effects,x,0");
      // 'graphValues' = Name of layer
      // 'Effects' = Name of propGroup
      // 'x' = Name of Slider
      // '0' = Index of Slider (This isn't needed for other props, like 'graphValues,Transform,Position')
      //
      this.animAPI.addValueCallback(xSlider, currentVal => {
        // We don't need the current value, so we just override it with some given variable in scope
        return this.x;
      });

      let otherSliders = ["y", "z"];
      otherSliders.forEach(slider => {
        let sliderControl = this.animAPI.getKeyPath(
          `graphValues,Effects,${slider},0`
        );
        this.animAPI.addValueCallback(sliderControl, currentVal => {
          return this[slider];
        });
      });
    },
    buildAnimation() {
      const self = this;
      const animData = {
        wrapper: self.elt,
        animType: "svg",
        loop: true,
        prerender: true,
        autoplay: true
      };
      animData.animationData = graph;
      return lottie.loadAnimation(animData);
    }
  }
};
</script>

<style>
svg {
  width: 100%;
}

.slottie-container {
  width: 100%;
  display: flex;
  justify-content: center;
}

.slottie-animation {
  width: 100%;
}

.anim-red {
  fill: #e57373;
}
.anim-green {
  fill: #81c784;
}
.anim-blue {
  fill: #64b5f6;
}
</style>
