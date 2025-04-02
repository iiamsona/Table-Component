<template>
    <div class="terminal-button-container">
        <div :class="status ? 'terminal-button-start': 'terminal-button-end'"><button  @click=changeState() class="round-btn"></button></div>
    </div>
</template>

<style lang="scss" scoped>
  @import "./index.scss";
</style>

<script>
export default {
props: {
  status: {
    type: Boolean,
    default: false
  },
},
data() {
  return {
    status: false
  }
},
methods: {
  changeState() {
    this.status = !this.status
  }
}
}
</script>