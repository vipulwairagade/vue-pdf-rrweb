<template>
  <div ref="viewer"></div>
</template>

<script>
/* eslint-disable */
import WebViewer from "@pdftron/webviewer";

export default {
  name: "WebViewer",
  props: {
    path: String,
    url: String,
  },
  mounted() {
    WebViewer(
      {
        path: this.path,
        initialDoc: this.url, // replace with your own PDF file
      },
      this.$refs.viewer
    ).then((instance) => {});
  },
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
div {
  width: 100%;
  height: 100vh;
}
</style>
