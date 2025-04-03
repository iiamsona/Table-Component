<template>
    <div class="main_table">
       <TableColumn />
       <TableColumn v-for="data in dataArray" :prop_checkbox="true" :prop_ID="data.id" :prop_name="data.name" :prop_address="data.address" :prop_phone="data.phone" :prop_email="data.email" :prop_website="data.website" :prop_org="data.owner" prop_status="ok" prop_terminal="ok" prop_action="ok"/>
      </div>
</template>

<script setup>
import TableColumn from '../tableColumn/TableColumn.vue'
import  {dataArray}  from '../../../data/index.js'
</script>

<style lang="scss" scoped>
  @import "./index.scss";
</style>

    