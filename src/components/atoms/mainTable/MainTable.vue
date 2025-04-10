<script setup>
import { ref, onMounted, onUnmounted } from "vue";
import TableColumn from "../tableColumn/TableColumn.vue";
import { dataArray, columnsArray } from "../../../data/index.js";

const visibleColumns = ref([]);

const updateVisibleColumns = () => {
  const saved = localStorage.getItem("columnVisibility");
  if (saved) {
    visibleColumns.value = JSON.parse(saved).filter(column => column.visible);
  }
};

onMounted(() => {
  updateVisibleColumns();
  window.addEventListener('storage', updateVisibleColumns);
});

onUnmounted(() => {
  window.removeEventListener('storage', updateVisibleColumns);
});
</script>

<template>
  <div class="main_table" :style="{ minWidth: `${visibleColumns.length * 90}px` }">
    <TableColumn :data="{}" :showCheckbox="true" />
    <TableColumn 
      v-for="data in dataArray" 
      :key="data.id" 
      :data="data" 
      :showCheckbox="true" 
    />
  </div>
</template>

<style lang="scss" scoped>
@import "./index.scss";
</style>
