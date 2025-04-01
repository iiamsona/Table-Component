<template>
    <div class="status-button">
        <p class="status-button_text">Active</p>
        <button class="status-button_btn"><img :src="arrow"></img></button>
    </div>
</template>

<style lang="scss" scoped>
  @import "./index.scss";
</style>

<script>
 import arrow from "../../../assets/arrow.svg";

 export default {
  data() {
    return {
        arrow
    }
  }
}
</script>