<script setup>
import { ref } from "vue";
import statusButton from "../statusButton/StatusButton.vue";
import terminalButton from "../terminalButton/TerminalButton.vue";
import actionButton from "../actionButton/ActionButton.vue";

const columnCount = ref(10);

const countColumns = () => {
  alert(columnCount.value);
};
</script>

<script>
export default {
  props: {
    prop_checkbox: { type: Boolean, default: false },
    prop_ID: { type: String, default: "ID" },
    prop_name: { type: String, default: "Name" },
    prop_address: { type: String, default: "Address" },
    prop_phone: { type: String, default: "Phone" },
    prop_email: { type: String, default: "Email" },
    prop_owner: { type: String, default: "Owner" },
    prop_room_max_count: { type: String, default: "Room Max Count" },
    prop_group_max_count: { type: String, default: "Group Max Count" },
    prop_responsible_max_count: {
      type: String,
      default: "Responsible Max Count",
    },
    prop_office_max_count: { type: String, default: "Office Max Count" },
    prop_day_sum: { type: String, default: "Day sum" },
    prop_total_sum: { type: String, default: "Total sum" },
    prop_deleted_at: { type: String, default: "Deleted at" },
    prop_created_at: { type: String, default: "Created at" },
    prop_updated_at: { type: String, default: "Updated at" },
    prop_isDefault: { type: String, default: "Is Default" },
    prop_employees: { type: Array, default: "Employees" },
    prop_website: { type: String, default: "Website" },
    prop_org: { type: String, default: "Organiz. type" },
    prop_status: { type: String, default: "Status" },
    prop_terminal: { type: String, default: "Terminal" },
    prop_action: { type: String, default: "Action" },
  },
  computed: {
    columnCount() {
      return Object.keys(this.$props).length;
    },
  },
};
</script>

<template>
  <div
    class="table_column"
    :style="{
      gridTemplateColumns: `repeat(${columnCount}, minmax(150px, 1fr))`,
    }"
  >
    <div v-if="prop_ID" class="table_column_item">
      <input
        type="checkbox"
        v-if="prop_checkbox"
        class="table_column_checkbox"
      />
      <p>{{ prop_ID }}</p>
    </div>
    <div v-if="prop_name" class="table_column_item">
      <p>{{ prop_name }}</p>
    </div>
    <div v-if="prop_address" class="table_column_item">
      <p>{{ prop_address }}</p>
    </div>
    <div v-if="prop_phone" class="table_column_item">
      <p>{{ prop_phone }}</p>
    </div>
    <div v-if="prop_email" class="table_column_item">
      <p>{{ prop_email }}</p>
    </div>
    <div v-if="prop_owner" class="table_column_item">
      <p>{{ prop_owner }}</p>
    </div>
    <div class="table_column_item">
      <p>{{ prop_org }}</p>
    </div>
    <div class="table_column_item">
      <p v-if="prop_status === 'Status'">Status</p>
      <statusButton v-else />
    </div>
    <div class="table_column_item">
      <p v-if="prop_terminal === 'Terminal'">Terminal</p>
      <terminalButton v-else />
    </div>
    <div class="table_column_item">
      <p v-if="prop_action === 'Action'">Action</p>
      <actionButton v-else />
    </div>
  </div>
</template>

<style lang="scss" scoped>
@import "./index.scss";
</style>
