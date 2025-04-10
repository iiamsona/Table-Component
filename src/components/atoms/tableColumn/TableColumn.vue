<script setup>
import { ref, computed, onMounted, onUnmounted } from "vue";
import statusButton from "../statusButton/StatusButton.vue";
import terminalButton from "../terminalButton/TerminalButton.vue";
import actionButton from "../actionButton/ActionButton.vue";
import moment from 'moment'

const props = defineProps({
  data: { type: Object, required: true },
  showCheckbox: { type: Boolean, default: false },
  isHeader: { type: Boolean, default: false },
});

  
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

const timeConvert = (date) => {
  return date ? moment(date).format("LL, H:mm") : "Invalid Date";
};

defineExpose({ timeConvert });

const ifDate = (column) => {
  if (column.key === "deleted_at" || column.key === "created_at" || column.key === "updated_at") {
    if (props.data[column.key] === undefined) {
      return column.label
    }
    return timeConvert(props.data[column.key]);
  }
  return props.data[column];
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
      gridTemplateColumns: `repeat(${visibleColumns.length}, minmax(90px, 1fr))`,
    }"
  >
    <div
      v-for="column in visibleColumns"
      :key="column.key"
      class="table_column_item"
    >
      <template v-if="props.isHeader && column.key != 'checkbox'">
        <p>{{ column.label }}</p>
      </template>

      <template v-else-if="column.key === 'checkbox'">
        <input type="checkbox" class="table_column_checkbox" />
      </template>

      <template v-else-if="column.key === 'status' && props.data[column.name] != null">
        <statusButton />
      </template>

      <template v-else-if="column.key === 'terminal'">
        <terminalButton />
      </template>

      <template v-else-if="column.key === 'action'">
        <actionButton />
      </template>

      <template v-else>
        <p>{{ ifArray(column.key) ?? ifDate(column) ?? props.data[column.key] ?? column.label }}</p>
      </template>
    </div>
  </div>
</template>


<style lang="scss" scoped>
@import "./index.scss";
</style>
