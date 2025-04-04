<script setup>
import { computed } from "vue";
import TableColumn from "../tableColumn/TableColumn.vue";
import { dataArray } from "../../../data/index.js";
import { columnsArray } from '../../../data/index.js';

const visibleColumns = computed(() => {
  return columnsArray.filter(column => column.visible);
});
</script>

<template>
<div class="main_table" :style="{ minWidth: `${visibleColumns.length * 90}px` }">
  <TableColumn :data="{}" :showCheckbox="true" />
    <TableColumn v-for="data in dataArray" :key="data.id" :data="data" :showCheckbox="true" />
  </div>
</template>

<style lang="scss" scoped>
@import "./index.scss";
</style>
