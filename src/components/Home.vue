<template>
  <div class="colors">
    <div
      v-for="color in colors"
      :key="color.red"
      :style="`background: rgb(${color.red}, ${color.green}, ${color.blue})`"
      class="color"
      @click="compareColors($event.target.style.backgroundColor)"
    />
  </div>
</template>

<script lang="ts">
import { Component, Vue } from "vue-property-decorator";

interface RGB {
  red: number;
  green: number;
  blue: number;
}

enum difficultyLevel {
  EASY = 3,
  MEDIUM = 6,
  HARD = 9
}

@Component({})
export default class Home extends Vue {
  MAX_RGB = 255;
  MIN_RGB = 0;

  colors: RGB[] = [];

  winner: string | null = null;

  difficulty: difficultyLevel = difficultyLevel.EASY;

  mounted() {
    const color = this.setColor();
    this.colors.push(color);

    this.winner = `rgb(${color.red}, ${color.green}, ${color.blue})`;

    this.generateColors(this.difficulty);
    this.sortColors();
  }

  compareColors(color: string) {
    console.log(color + " - " + this.winner);
    if (color === this.winner) {
      console.log("win");
    }
  }

  sortColors(): void {
    this.colors.sort((a, b) => {
      return a.red - b.red;
    });
  }

  generateColors(amount: number) {
    for (let i = 0; i < amount; i++) {
      const color = this.setColor();
      this.colors.push(color);
    }
  }

  setColor(): RGB {
    const color: RGB = {
      red: this.getRandom(),
      green: this.getRandom(),
      blue: this.getRandom()
    };

    return color;
  }

  getRandom(): number {
    return (
      Math.floor(Math.random() * (this.MAX_RGB - this.MIN_RGB + 1)) +
      this.MIN_RGB
    );
  }
}
</script>

<style scoped lang="scss">
.colors {
  display: flex;
  flex-direction: column;
}

.color {
  width: 100%;
  height: 100%;
}
</style>
