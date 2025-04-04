<script setup>
import { computed } from "vue";
import statusButton from "../statusButton/StatusButton.vue";
import terminalButton from "../terminalButton/TerminalButton.vue";
import actionButton from "../actionButton/ActionButton.vue";
import { columnsArray } from '../../../data/index.js';

const props = defineProps({
  data: { type: Object, required: true },
  showCheckbox: { type: Boolean, default: false },
});

const visibleColumns = computed(() => {
  return columnsArray.filter(column => column.visible);
});
</script>

<template>
  <div class="table_column" :style="{
      gridTemplateColumns: `repeat(${visibleColumns.length}, minmax(150px, 1fr))`,
    }">
    <div v-for="column in visibleColumns" :key="column.key" class="table_column_item">
      <template v-if="column.key === 'checkbox'">
        <input type="checkbox" class="table_column_checkbox" />
      </template>
      <template v-else-if="column.key === 'status'">
        <statusButton />
      </template>
      <template v-else-if="column.key === 'terminal'">
        <terminalButton />
      </template>
      <template v-else-if="column.key === 'action'">
        <actionButton />
      </template>
      <template v-else>
        <p>{{ props.data[column.key] || column.label }}</p>
      </template>
    </div>
  </div>
</template>

<style lang="scss" scoped>
@import "./index.scss";
</style>
