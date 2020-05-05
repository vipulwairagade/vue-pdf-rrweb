<template>
  <div id="app">
    <p>{{ count }}</p>
    <button @click="stopRecord">replay</button>
    <WebViewer
      :path="`${publicPath}lib`"
      url="https://pdftron.s3.amazonaws.com/downloads/pl/webviewer-demo.pdf"
    />
  </div>
</template>

<script>
import WebViewer from "./components/WebViewer.vue";

export default {
  name: "app",
  components: {
    WebViewer,
  },
  data() {
    return {
      publicPath: process.env.BASE_URL,
      count: 0,
    };
  },
  mounted() {
    const self = this;
    this.events = [];
    this.stopper = rrweb.record({
      emit(event) {
        self.events.push(event);
      },
    });
    // do some thing to update the view
    this.timer = setInterval(() => {
      this.count++;
    }, 1000);
  },
  methods: {
    stopRecord() {
      this.stopper();
      clearInterval(this.timer);
      const replayer = new rrweb.Replayer(this.events);
      replayer.play();
    },
  },
};
</script>

<style>
#app {
  font-family: "Avenir", Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}
</style>
