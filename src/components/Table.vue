<template>
  <div id="table">
    <div>
      <div id="tableHeader" class="tableRow">
        <div class="cell stock">Stock</div>
        <div class="cell">Current</div>
        <div class="cell change">Change</div>
      </div>
      <Item
        v-for="(item, index) in values" :key="index"
        v-bind:item="item" />
    </div>
  </div>
</template>

<script>
import Item from '@/components/Item'

export default {
  name: 'Table',
  props: ['values'],
  components: {
    Item
  }
}
</script>

<style lang="scss">
#table {
  margin: 2rem auto;
  width: fit-content;
  #tableHeader{
    background: #f5f5f5;
    font-weight: bold;
    .cell{
      color: #2c3e50;
    }
  }
  .tableRow {
  display: flex;
  }
  .cell {
    padding: 1rem;
    width: 100px;
    border: 1px solid #eeeeee;
  }
}
</style>
