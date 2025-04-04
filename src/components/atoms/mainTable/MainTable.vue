<script setup>
import TableColumn from "../tableColumn/TableColumn.vue";
import { dataArray } from "../../../data/index.js";
</script>

<template>
  <div class="main_table">
    <TableColumn :data="{}" :showCheckbox="true" />
    <TableColumn v-for="data in dataArray" :key="data.id" :data="data" :showCheckbox="true" />
  </div>
</template>

<style lang="scss" scoped>
@import "./index.scss";
</style>
