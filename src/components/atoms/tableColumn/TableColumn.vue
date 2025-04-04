<script setup>
import { computed } from "vue";
import statusButton from "../statusButton/StatusButton.vue";
import terminalButton from "../terminalButton/TerminalButton.vue";
import actionButton from "../actionButton/ActionButton.vue";
import { columnsArray } from "../../../data/index.js";
import moment from 'moment'

const props = defineProps({
  data: { type: Object, required: true },
  showCheckbox: { type: Boolean, default: false },
});

const visibleColumns = computed(() => {
  return columnsArray.filter((column) => column.visible);
});

const timeConvert = (date) => {
  return date ? moment(date).format("LL, H:mm") : "Invalid Date";
};

defineExpose({ timeConvert });

const ifDate = (key) => {
  if (key === "deleted_at" || key === "created_at") {
    return timeConvert(props.data[key]);
  }
  return props.data[key];
};

const ifArray = (key) => {
  if (key === "employees") {
    const value = props.data[key];

    if (Array.isArray(value)) {
      return value.map((item) => item.name || item).join(", ");
    }

    if (typeof value === "object" && value !== null) {
      return value.name || JSON.stringify(value);
    }
  }

  return null;
};

</script>

<template>
  <div
    class="table_column"
    :style="{
      gridTemplateColumns: `repeat(${visibleColumns.length}, minmax(150px, 1fr))`,
    }"
  >
    <div
      v-for="column in visibleColumns"
      :key="column.key"
      class="table_column_item"
    >
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
        <p>{{ ifArray(column.key) ?? ifDate(column.key) ?? props.data[column.key] ?? column.label }}</p>
      </template>
    </div>
  </div>
</template>

<style lang="scss" scoped>
@import "./index.scss";
</style>
