<template>
  <div class="wrapper">
    <div v-if="loading === true">
      <p>loading....</p>
    </div>
    <div v-else>
      <div v-if="error === false">
        <button type="submit" @click.prevent="myTest()" class="btn">get data</button>


        <div class="table">
          <div class="row">
            <div class="column-header">Stack</div>
            <div class="column-header">Current</div>
            <div class="column-header">Change</div>
          </div>

          <div v-for="(arr, index) in newArray" :key="index" class="row-data">
            <div class="row-data-inner">
              {{ arr.s }}
            </div>
            <div class="row-data-inner">
              {{ arr.c | dataFixed() }}
            </div>
            <div class="row-data-inner"
                 :class="{negative: Math.sign(arr.st) === -1 }">
              {{ arr.st | dataFixed() }}
            </div>
          </div>
        </div>
      </div>
      <div v-else>
        <p>no data</p>
      </div>
    </div>
  </div>
</template>

<script>
import simulateAsyncReq from '@/plugins/getDataFunc'
import {payload} from '@/mocData/index'

export default {
  data()
  {
    return {
      globalData: {},
      current: '',
      start: '',
      stocks: '',
      negative: false,
      newArray: [],
      error: false,
      loading: false
    }
  },
  name: "DataCurrency",
  filters: {
    dataFixed(value)
    {
      return value.toFixed(2)
    },
  },
  methods: {
    myTest()
    {
      simulateAsyncReq(payload)
          .then(r =>
          {
            this.loading = true
            setTimeout(() =>
            {
              this.current = r.current
              this.start = r.start
              this.stocks = r.stocks

              let arrLength = r.current.length
              for (let i = 0; i < arrLength; i++)
              {
                this.newArray[i] = {
                  s: this.stocks[i],
                  c: this.current[i],
                  st: this.start[i]
                }
              }
              this.loading = false
             this.newArray.sort((a, b) => a.s > b.s ? 1 : -1)
            }, 1000)

          }).catch(() => this.error = true)

    },
  }

}
</script>

<style lang="sass" scoped>
.table
  justify-content: center
  display: flex
  flex-direction: column

.btn
  font-size: 1.1rem
  padding: .5rem 2rem
  border: 1px solid #d7d7d7
  transition: all .5s ease
  border-radius: 3px
  margin-bottom: 3rem

  &:hover
    background: #589fa0

  &:focus
    outline: none

.row
  display: flex

.column-header
  background: #d7d7d7
  padding: 1rem
  color: black
  font-weight: bold

.row-data
  display: flex
  justify-content: space-between

.row-data-inner
  padding: 1rem

.negative
  color: red
</style>