<template>
  <div class="customize-button">
    <button @click="open = !open" class="customize-button-btn">
      <p>Filter</p>
      <img :src="more" />
    </button>
    <div class="customize-button-container" v-show="open">
      <div v-for="column in columns" :key="column.key" class="customize-button-div">
        <div class="customize-button-column">
          <input
            type="checkbox"
            :value="column.key"
            v-model="column.visible"
            @change="handleVisibilityChange"
          />
          <p>{{ column.label }}</p>
        </div>
      </div>
    </div>
  </div>
</template>

<script setup>
import { ref, reactive, onMounted } from 'vue';
import more from '../../../assets/more.svg';
import { columnsArray } from '../../../data/index.js';

const open = ref(false);
const columns = reactive(columnsArray);

const handleVisibilityChange = () => {
  localStorage.setItem('columnVisibility', JSON.stringify(columns));
  window.dispatchEvent(new Event('storage'));
};

onMounted(() => {
  const savedColumns = localStorage.getItem('columnVisibility');
  if (savedColumns) {
    const parsed = JSON.parse(savedColumns);
    Object.assign(columns, parsed);
  }
});
</script>

<style lang="scss" scoped>
@import "./index.scss";
</style>
