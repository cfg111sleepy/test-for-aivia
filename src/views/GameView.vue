<template>
  <v-container class="app">
    <h2>Size X:</h2>
    <v-text-field v-model.number="sizeX" type="number" min="1" @input="drawSquares"></v-text-field>
    <h2>Size Y:</h2>
    <v-text-field v-model.number="sizeY" type="number" min="1" @input="drawSquares"></v-text-field>

    <v-container class="grid-container">
      <v-row v-for="(row, rowIndex) in grid" :key="rowIndex" class="row">
        <v-col v-for="(cell, cellIndex) in row" :key="cellIndex" class="cell" :class="{ blue: cell.isBlue }"
          @mouseover="toggleColor(cell)">
        </v-col>
      </v-row>
    </v-container>
  </v-container>
</template>

<script>
import { ref, watch } from 'vue';

export default {
  setup() {
    const sizeX = ref(1);
    const sizeY = ref(1);
    const grid = ref([]);

    const drawSquares = () => {
      grid.value = [];
      for (let i = 0; i < sizeY.value; i++) {
        const row = [];
        for (let j = 0; j < sizeX.value; j++) {
          row.push({ isBlue: false });
        }
        grid.value.push(row);
      }
    };

    const toggleColor = (cell) => {
      cell.isBlue = !cell.isBlue;
    };

    watch([sizeX, sizeY], drawSquares, { immediate: true });

    return {
      sizeX,
      sizeY,
      grid,
      toggleColor,
    };
  },
};
</script>

<style>
.app {
  display: flex;
  flex-direction: column;
  align-items: center;
  margin-top: 3rem;
}

h2 {
  margin: 1rem 0;
}

.grid-container {
  background-color: #333;
  margin-top: 1.5rem;
}

.row {
  display: flex;
}

.cell {
  width: 2.25rem;
  height: 2.25rem;
  margin: 0.063rem;
  cursor: pointer;
  background-color: #fff;
}

.blue {
  background-color: blue;
}
</style>
