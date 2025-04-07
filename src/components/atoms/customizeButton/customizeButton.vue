<template>
    <div class="customize-button">
      <button @click="open = !open" class="customize-button-btn">
        <p>Filter</p>
        <img :src="more" />
      </button>
      <div class="customize-button-container" v-show="open">
        <div v-for="column in columnsArray" :key="column.key" class="customize-button-div">
          <div class="customize-button-column">
            <input
              type="checkbox"
              :value="column.key"
              v-model="column.visible"
              @change="saveVisibility"
            />
            <p>{{ column.label }}</p>
          </div>
        </div>
      </div>
    </div>
  </template>
  
  <script setup>
  import { ref, onMounted, watch } from 'vue';
  import more from '../../../assets/more.svg';
  import { columnsArray } from '../../../data/index.js';
  
  const open = ref(false);
  
  const saveVisibility = () => {
    const visibilityMap = columnsArray.reduce((acc, col) => {
      acc[col.key] = col.visible;
      return acc;
    }, {});
    localStorage.setItem('columnVisibility', JSON.stringify(visibilityMap));
  };
  
  onMounted(() => {
    const saved = localStorage.getItem('columnVisibility');
    if (saved) {
      const visibilityMap = JSON.parse(saved);
      columnsArray.forEach(col => {
        if (visibilityMap.hasOwnProperty(col.key)) {
          col.visible = visibilityMap[col.key];
        }
      });
    }
  });
  </script>
  
  <style lang="scss" scoped>
  @import "./index.scss";
  </style>
  