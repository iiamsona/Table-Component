<template>
    <div class="customize-button">
        <button @click="open = !open" class="customize-button-btn">
            <p>Filter</p>
            <img :src="more"></img>
        </button>
        <div class="customize-button-container">
            <div v-if="open === true" v-for="column in columnsArray" :key="column.key" class="customize-button-div">
                <div class="customize-button-column">
                    <input type="checkbox" :value="column.key" v-model="column.visible" />
                    <p>{{column.label}}</p>
                </div>
            </div>
        </div>
    </div>
</template>

<script setup>
import { ref } from 'vue';
import more from '../../../assets/more.svg'
import { columnsArray } from "../../../data/index.js";

const open = ref(false);
</script>


<style lang="scss" scoped>
  @import "./index.scss";
</style>