<template>
  <div id="app">
    <HighlightCode />
  </div>
</template>

<script>
import HighlightCode from "@/components/HighlightCode.vue";
import watermark from "@/utils/warterMark";

export default {
  name: "App",
  data() {
    return {};
  },
  components: {
    HighlightCode,
  },
  mounted() {
    watermark.set("zpgong");
  },
  methods: {},
};
</script>
<style>
#app, body, html{
  /* background-color: hsl(220, 13%, 18%); */
}
</style>
