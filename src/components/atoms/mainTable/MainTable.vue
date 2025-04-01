<template>
    <div class="main_table">
       <TableColumn />
       <TableColumn prop_ID="ok" prop_name="ok" prop_address="ok" prop_phone="ok" prop_email="ok" prop_website="ok" prop_org="ok" prop_status="ok" />
    </div>
</template>

<script setup>
import TableColumn from '../tableColumn/TableColumn.vue'
</script>

<style lang="scss" scoped>
  @import "./index.scss";
</style>