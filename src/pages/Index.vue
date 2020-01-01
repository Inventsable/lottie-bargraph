<template>
  <q-page class="flex flex-center">
    <graph />
  </q-page>
</template>

<script>
export default {
  name: "PageIndex",
  components: {
    graph: require("src/components/graph.vue").default
  }
};
</script>
