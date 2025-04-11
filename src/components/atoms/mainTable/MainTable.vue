<script setup>
import { ref, onMounted, onUnmounted } from "vue";
import TableColumn from "../tableColumn/TableColumn.vue";
import TableCard from "../tableColumn/TableCard.vue";
import { dataArray, columnsArray } from "../../../data/index.js";

const visibleColumns = ref([]);
const card = ref(true); 

const updateVisibleColumns = () => {
  const saved = localStorage.getItem("columnVisibility");
  if (saved) {
    visibleColumns.value = JSON.parse(saved).filter(column => column.visible);
  }
};

const updateCardView = () => {
  const stored = localStorage.getItem("card");
  if (stored !== null) {
    card.value = JSON.parse(stored);
  }
};

onMounted(() => {
  updateVisibleColumns();
  updateCardView();
  window.addEventListener("storage", () => {
    updateVisibleColumns();
    updateCardView();
  });
});

onUnmounted(() => {
  window.removeEventListener("storage", updateVisibleColumns);
});
</script>

<template>
  <div class="main_table" :style="{ minWidth: `${visibleColumns.length * 85}px` }">
    <div v-if="!card">
      <TableColumn :data="{}" :showCheckbox="true" :isHeader="true" />
      <TableColumn 
        v-for="data in dataArray" 
        :key="data.id" 
        :data="data" 
        :showCheckbox="true" 
      />
    </div>
    <div v-else :style="{ display: 'flex' }">
      <TableCard 
        v-for="data in dataArray" 
        :key="data.id" 
        :data="data" 
        :showCheckbox="true" 
      />
    </div>
  </div>
</template>
