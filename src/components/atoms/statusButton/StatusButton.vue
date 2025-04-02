<template>
  <div class="status-button-container">
    <div v-if = "status == false" class="status-button-inactive">
      <p class="status-button_text-inactive">Inactive</p>
      <button @click=openStatus() class="status-button_btn"><img :src="arrow"></img></button>
    </div>
    <div v-else-if="status == true" class="status-button-active">
      <p class="status-button_text-active">Active</p>
      <button @click=openStatus() class="status-button_btn"><img :src="arrow"></img></button>
    </div>
    <div v-if="open == true" class="change-status-container">
      <p :class="status ? 'change-status-selected' : 'change-status'" @click=changeActiveStatus()>Active</p>
      <p :class="status ? 'change-status' : 'change-status-selected'" @click=changeInactiveStatus()>Inactive</p>
    </div>
  </div>
</template>

<style lang="scss" scoped>
  @import "./index.scss";
</style>

<script>
 import arrow from "../../../assets/arrow.svg";

 export default {
  props: {
    status: {
      type: Boolean,
      default: true
    },
    open:{
      type:Boolean,
      default: false
    }
  },
  data() {
    return {
        arrow,
        status,
        open
    }
  },
  methods:{
    changeActiveStatus(){
      this.status = true;
    },
    changeInactiveStatus(){
      this.status = false;
    },
    openStatus(){
      this.open = !this.open;
    }
  }
}
</script>
