<template>
  <div id="app">
    <img alt="Vue logo" src="./assets/peiko-logo-mini.png">
    <h1>Test</h1>
    <hr>
    <Button
      v-bind:getServerData="getServerData" />
    <ErrorMessage v-if="isError" />
    <Loader v-if="!isLoaded" />
    <Table
      v-if="values.length > 0 && !isError && isLoaded"
      v-bind:values="values"
    />
    
  </div>
</template>

<script>
import { payload } from '@/mocData/index.js'
import simulateAsyncReq from '@/plugins/getDataFunc.js'
import Table from '@/components/Table'
import Loader from '@/components/Loader'
import Button from '@/components/Button'
import ErrorMessage from '@/components/ErrorMessage'

export default {
  name: 'App',
  data() {
    return {
      values: {},
      isError: false,
      isLoaded: true
    }
  },
  components: {
    Button,
    Table,
    Loader,
    ErrorMessage
  },
  methods: {
    reformResponce: (resValues) => {
      let unsortedValues = []
      for (let i = 0; i < resValues.stocks.length; i++){
          unsortedValues.push({
            'stock': resValues.stocks[i],
            'current': resValues.current[i],
            'start': resValues.start[i]
            })
        }
        return unsortedValues
    },
    sortValues: (unsortedValues) => {
      return unsortedValues.sort((a, b) => {
          let stockA = a.stock.toUpperCase()
          let stockB = b.stock.toUpperCase()
          return (stockA < stockB) ? -1 : 1
          })
    },
    async getServerData() {
      try{
        this.isLoaded = false
        this.isError = false

        const res = await simulateAsyncReq(payload)
        const resValues = await res
        
        this.values = 
          this.sortValues(
            this.reformResponce(resValues))

        this.isError = false
        this.isLoaded = true
      } catch(err) {
        this.isError = true
        this.isLoaded = true
      }
    }
  }
}
</script>

<style lang="scss">
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
