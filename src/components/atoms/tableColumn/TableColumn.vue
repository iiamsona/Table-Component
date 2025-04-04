<script setup>
import { computed } from "vue";
import statusButton from "../statusButton/StatusButton.vue";
import terminalButton from "../terminalButton/TerminalButton.vue";
import actionButton from "../actionButton/ActionButton.vue";

const props = defineProps({
  prop_checkbox: { type: Boolean, default: false },
  prop_ID: { type: String, default: "ID" },
  prop_name: { type: String, default: "Name" },
  prop_address: { type: String, default: "Address" },
  prop_phone: { type: String, default: "Phone" },
  prop_email: { type: String, default: "Email" },
  prop_owner: { type: String, default: "Owner" },
  prop_room_max_count: { type: String, default: "Room Max Count" },
  prop_group_max_count: { type: String, default: "Group Max Count" },
  prop_responsible_max_count: { type: String, default: "Responsible Max Count" },
  prop_office_max_count: { type: String, default: "Office Max Count" },
  prop_day_sum: { type: String, default: "Day sum" },
  prop_total_sum: { type: String, default: "Total sum" },
  prop_deleted_at: { type: String, default: "Deleted at" },
  prop_created_at: { type: String, default: "Created at" },
  prop_updated_at: { type: String, default: "Updated at" },
  prop_isDefault: { type: String, default: "Is Default" },
  prop_employees: { type: Array, default: () => [] },
  prop_status: { type: String, default: "Status" },
  prop_terminal: { type: String, default: "Terminal" },
  prop_action: { type: String, default: "Action" }
});

const defaultValues = {
  prop_checkbox: false,
  prop_ID: "ID",
  prop_name: "Name",
  prop_address: "Address",
  prop_phone: "Phone",
  prop_email: "Email",
  prop_owner: "Owner",
  prop_room_max_count: "Room Max Count",
  prop_group_max_count: "Group Max Count",
  prop_responsible_max_count: "Responsible Max Count",
  prop_office_max_count: "Office Max Count",
  prop_day_sum: "Day sum",
  prop_total_sum: "Total sum",
  prop_deleted_at: "Deleted at",
  prop_created_at: "Created at",
  prop_updated_at: "Updated at",
  prop_isDefault: "Is Default",
  prop_employees: [],
  prop_status: "Status",
  prop_terminal: "Terminal",
  prop_action: "Action"
};

const filteredProps = computed(() => {
  return Object.entries(props)
    .filter(([key, value]) => JSON.stringify(value) !== JSON.stringify(defaultValues[key]))
    .map(([key]) => key);
});

const columnCount = computed(() => filteredProps.value.length);
</script>

<template>
  <div
    class="table_column"
    :style="{
      gridTemplateColumns: `repeat(${columnCount}, minmax(150px, 1fr))`,
    }"
  >
    <div v-for="prop in filteredProps" :key="prop" class="table_column_item">
      <template v-if="prop === 'prop_checkbox'">
        <input type="checkbox" class="table_column_checkbox" />
      </template>
      <template v-else-if="prop === 'prop_status'">
        <statusButton />
      </template>
      <template v-else-if="prop === 'prop_terminal'">
        <terminalButton />
      </template>
      <template v-else-if="prop === 'prop_action'">
        <actionButton />
      </template>
      <template v-else>
        <p>{{ props[prop] }}</p>
      </template>
    </div>
  </div>
  <div>
    {{ filteredProps }}
  </div>
</template>

<style lang="scss" scoped>
@import "./index.scss";
</style>
