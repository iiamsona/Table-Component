<template>
  <div>
    <div v-if = "!status" class="status-button-inactive">
      <p class="status-button_text-inactive">Inactive</p>
      <button @click=changeStatus() class="status-button_btn"><img :src="arrow"></img></button>
    </div>
    <div v-else class="status-button-active">
        <p class="status-button_text-active">Active</p>
          <button @click=changeStatus() class="status-button_btn"><img :src="arrow"></img></button>
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
    }
  },
  data() {
    return {
        arrow,
        status
    }
  },
  methods:{
    changeStatus(){
      this.status = !this.status;
      console.log(this.status);
    }
  }
}
</script>