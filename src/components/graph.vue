<template>
  <div class="graph-wrapper">
    <span class="text-h4 flex justify-center">simple graph</span>
    <div class="graph-item">
      <slottie :x="x" :y="y" :z="z" />
    </div>
    <div class="knob-wrapper">
      <q-knob
        :min="0"
        :max="30"
        v-model="x"
        show-value
        size="50px"
        :thickness="0.22"
        color="red-4"
        track-color="grey-3"
        class="q-ma-md"
      />
      <q-knob
        :min="0"
        :max="30"
        v-model="y"
        show-value
        size="50px"
        :thickness="0.22"
        color="green-4"
        track-color="grey-3"
        class="q-ma-md"
      />
      <q-knob
        :min="0"
        :max="30"
        v-model="z"
        show-value
        size="50px"
        :thickness="0.22"
        color="blue-4"
        track-color="grey-3"
        class="q-ma-md"
      />
    </div>
  </div>
</template>

<script>
export default {
  data: () => ({
    x: 20,
    y: 5,
    z: 15
  }),
  components: {
    slottie: require("./slottie.vue").default
  }
};
</script>


<style>
.knob-wrapper {
  padding-left: 38px;
}

.graph-item,
.knob-wrapper {
  width: 300px;
}
</style>