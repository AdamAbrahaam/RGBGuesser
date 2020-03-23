<template>
  <div id="app" class="sides">
    <Home class="side" />
    <div class="side">a</div>
  </div>
</template>

<script lang="ts">
import { Component, Vue } from "vue-property-decorator";
import Home from "@/components/Home.vue";

@Component({
  components: {
    Home
  }
})
export default class App extends Vue {}
</script>

<style lang="scss">
.sides {
  display: flex;
  flex-direction: row;

  width: 100%;
  height: 100%;
}

.side {
  width: 50vw;
  height: 100vh;
}

body {
  margin: 0;
  padding: 0;
}

#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}
</style>
