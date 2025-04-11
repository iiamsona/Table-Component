
<template>
  <div :style="{ display: 'flex', justifyContent: 'start', alignItems: 'end' }">
      <CustomizeButton/>
    <CardButton/>
    </div>
    <MainTable />
</template>
 

<script setup>
import CustomizeButton from './components/atoms/customizeButton/customizeButton.vue';
import MainTable from './components/atoms/mainTable/MainTable.vue';
import CardButton from './components/atoms/cardButton/cardButton.vue';
</script>