<template>
  <button
    id="getDataButton"
    v-on:click="getServerData">
    Get data
  </button>
</template>

<script>

export default {
  name: 'Button',
  props: ['getServerData']
}
</script>

<style lang="scss">
#getDataButton {
  font-size: 0.9rem;
  font-weight: bold;
  padding: 0.5rem 2rem;
  background: #f5f5f5;
  color: #2c3e50;
  border: 1px solid #eeeeee;
  &:hover{
    cursor: pointer;
    background: #E5E5E5;
  }
}
</style>
