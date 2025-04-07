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
  localStorage.setItem('columnVisibility', JSON.stringify(columnsArray));
};

  
  </script>
  
  <style lang="scss" scoped>
  @import "./index.scss";
  </style>
  