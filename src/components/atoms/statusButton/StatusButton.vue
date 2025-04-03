<template>
  <div class="status-button-container">
    <div v-if = "status == false" class="status-button-inactive">
      <p class="status-button_text-inactive">Inactive</p>
      <button v-if="open" @click=openStatus() class="status-button_btn"><img :src="openIcon"></img></button>
      <button v-else @click=openStatus() class="status-button_btn"><img :src="closeIcon"></img></button>
    </div>
    <div v-else-if="status == true" class="status-button-active">
      <p class="status-button_text-active">Active</p>
      <button v-if="open" @click=openStatus() class="status-button_btn"><img :src="openIcon"></img></button>
      <button v-else @click=openStatus() class="status-button_btn"><img :src="closeIcon"></img></button>
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
 import openIcon from "../../../assets/icon_chev_open.svg";
 import closeIcon from "../../../assets/icon_chev_close.svg";

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
        openIcon,
        closeIcon,
        status:true,
        open:false
    }
  },
  methods:{
    changeActiveStatus(){
      this.status = true;
      this.open = false;
    },
    changeInactiveStatus(){
      this.status = false;
      this.open = false;
    },
    openStatus(){
      this.open = !this.open;
    }
  }
}

</script>
