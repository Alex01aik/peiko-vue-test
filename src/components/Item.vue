<template>
  <div class="tableRow">
    <div class="cell stock">{{item.stock}}</div>
    <div class="cell">{{putComa(item.current.toFixed(2))}}</div>
    <div  class="cell change"
      v-bind:class="{negative: isNegative}">
      <span v-if="!isNegative">+</span>
      <span>{{putComa((item.current - item.start).toFixed(2))}}</span>
    </div>
  </div>
</template>

<script>

export default {
  name: 'Item',
  props: ['item'],
  computed: {
    isNegative() {
      return this.item.current - this.item.start < 0
    }
  },
  methods: {
    putComa(value) {
      if (value.toString().split('.')[0].slice(-4, -3)) {
        let int = value.toString().split('.')[0]
        let fract = value.toString().split('.')[1]
        let intWithComa = 
          `${int.substr(0, int.length - 3)},${int.substr(int.length - 3, int.length)}`
        return `${intWithComa}.${fract}`
      } else {
        return value
      }
    }
  }
}
</script>

<style lang="scss">
.stock{
  text-align: left;
}
.change{
  color: green;
  text-align: right;
}
.negative {
  color: red;
}
</style>
