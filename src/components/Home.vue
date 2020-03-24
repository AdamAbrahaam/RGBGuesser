<template>
  <div class="colors">
    <div
      v-for="color in colors"
      :key="color.red"
      :style="`background: rgb(${color.red}, ${color.green}, ${color.blue})`"
      class="color"
      @click="compareColors($event.target)"
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
  EASY = 2,
  MEDIUM = 5,
  HARD = 7
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

  compareColors(target: HTMLElement): void {
    const color = target.style.backgroundColor;
    console.log(target);
    if (color === this.winner) {
      this.setBackground(target);
    }
  }

  setBackground(target: HTMLElement): void {
    const background = document.getElementById("background");

    if (!background) {
      return;
    }

    background.style.background = target.style.backgroundColor;
    background.style.left = `${target.offsetLeft}px`;
    background.style.top = `${target.offsetTop}px`;
    background.style.transform = "scale(25)";
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
  flex-direction: row;
  justify-content: space-around;
  align-items: flex-end;
}

.color {
  width: 100px;
  height: 100px;
  display: block;
  border-radius: 50%;
  margin: 30px;
  cursor: pointer;
}
</style>
