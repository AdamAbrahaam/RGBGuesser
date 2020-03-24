<template>
  <div id="app">
    <div id="background" />

    <div class="sides">
      <div class="logo">RGB Guesser</div>
      <div class="picker">
        Pick a color
        <Home />
      </div>
    </div>
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
#background,
.sides {
  position: absolute;
}

#background {
  width: 100px;
  height: 100px;
  display: block;
  border-radius: 50%;

  transition: transform 2s;
  transform-origin: center center;
}

.sides {
  display: flex;
  flex-direction: column;

  width: 100%;
  height: 100%;
}

.logo {
  height: 40vh;
}

.picker {
  margin: auto;
  width: auto;
  height: 60vh;
}

body {
  margin: 0;
  padding: 0;
  overflow: hidden;
}

#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}
</style>
