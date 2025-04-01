<template>
    <div class="table_column">
        <div class="table_column_item">
            <input type="checkbox" class="table_column_checkbox" />
            <p>{{ prop_ID }}</p>
        </div>
        <div class="table_column_item">
            <p>{{ prop_name }}</p>
        </div>
        <div class="table_column_item">
            <p>{{ prop_address }}</p>
        </div>
        <div class="table_column_item">
            <p>{{ prop_phone }}</p>
        </div>
        <div class="table_column_item">
            <p>{{ prop_email }}</p>
        </div>
        <div class="table_column_item">
            <p>{{ prop_website }}</p>
        </div>
        <div class="table_column_item">
            <p>{{ prop_org }}</p>
        </div>
        <div class="table_column_item">
            <p v-if="prop_status === 'Status'">Status</p>
            <div v-else>
                <statusButton/>
            </div>
        </div>
        <div class="table_column_item">
            Terminal
        </div>
        <div class="table_column_item">
            Action
        </div>
    </div>
</template>

<script setup>
import statusButton from '../statusButton/StatusButton.vue'
</script>

<script>
export default {
  props: {
    prop_ID: {
      type: String,
      default: 'ID'
    },
    prop_name: {
      type: String,
      default: 'Name'
    },
    prop_address: {
      type: String,
      default: 'Address'
    },
    prop_phone: {
      type: String,
      default: 'Phone'
    },
    prop_email: {
      type: String,
      default: 'Email'
    },
    prop_website: {
      type: String,
      default: 'Website'
    },
    prop_org: {
      type: String,
      default: 'Organiz. type'
    },
    prop_status: {
      type: String,
      default: 'Status'
    }
  }
}
</script>

<style lang="scss" scoped>
  @import "./index.scss";
</style>