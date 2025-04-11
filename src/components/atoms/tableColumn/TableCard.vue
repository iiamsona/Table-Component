<script setup>
import { ref, computed, onMounted, onUnmounted } from "vue";
import statusButton from "../statusButton/StatusButton.vue";
import terminalButton from "../terminalButton/TerminalButton.vue";
import actionButton from "../actionButton/ActionButton.vue";
import moment from 'moment'
import sort from '../../../assets/icon_sort.svg'

const props = defineProps({
  data: { type: Object, required: true },
  showCheckbox: { type: Boolean, default: false },
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
    <div class="card_wrapper">
    <div class="table_card">
        <div
        class="card_item"
        v-for="column in visibleColumns"
        :key="column.key"
        >
        <div>
          
        </div>
        <template v-if="column.key === 'checkbox'">
          <div class="card_header">
            <input type="checkbox" class="table_column_checkbox" />
        </div>
      </template>
      
      <template v-else>
        <div class="label">{{ column.label }}</div>
        <div class="value">
          <template v-if="column.key === 'status'">
            <statusButton />
          </template>
          
          <template v-else-if="column.key === 'terminal'">
            <terminalButton />
          </template>
          
          <template v-if="column.key === 'action'" :styles>
              <actionButton />
            </template>
            <template v-else>
              {{ ifArray(column.key) ?? ifDate(column) ?? props.data[column.key] ?? '—' }}
            </template>
          </div>
        </template>
      </div>
    </div>
</div>
  </template>
  


<style lang="scss" scoped>
@import "./card.scss";
</style>
