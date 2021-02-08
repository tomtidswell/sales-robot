<template>
  <section class="products">
    <div class="section">
      <div class="columns">
        <div class="column">
          <div class="subtitle">
            {{ retailerData.displayName }}
          </div>
        </div>
        <Filters class="column" @sort="handleSort" />
        <b-button class="refresh" @click="refreshData">
          Refresh data
        </b-button>
      </div>
    </div>
    <div class="grid">
      <Product
        v-for="product in productData"
        :key="product._id"
        :data="product"
      />
    </div>
  </section>
</template>

<script>

import _ from 'lodash'
import { retailerConfig } from '../assets/config'
import Product from '../components/Product'
import Filters from '../components/Filters'

export default {
  name: 'ProductsByRetailer',
  components: {
    Product,
    Filters
  },
  props: {
  },
  data () {
    return {
      productDataResponse: [],
      productData: []
    }
  },
  computed: {
    retailer () {
      return this.$route.params.id
    },
    retailers () {
      return retailerConfig
    },
    retailerData () {
      return this.retailers[this.retailer] || {}
    }
  },
  watch: {
    '$route.params' () {
      this.getData()
    }
  },
  created () {
    this.getData()
  },
  methods: {
    refreshData () {
      this.getData()
    },
    async getData () {
      const res = await fetch(`https://sharp-turing-d1c0f9.netlify.app/api/retailer/${this.retailer}`)
      // console.log("Endpoint response:", res)
      this.productDataResponse = res.status === 200 ? await res.json() : []
      // console.log("Data:", this.productData)
      // this.productDataResponse = _.filter(this.productDataResponse, 'price') //make sure we have price data for the item
      this.handleSort(['score', 'desc'])
      // console.log("Sorted data:", this.productData)
    },
    handleSort (e) {
      const [field, direction] = e
      console.log(field, direction)
      this.productData = _.orderBy(this.productDataResponse, field, direction)
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style lang="scss">
a {
  color: #42b983;
}
.subtitle{
  font-size: 1.8rem;
}
section.products{
    display: flex;
    flex-direction: column;
}
.grid {
  display: grid;
  grid-template-columns: repeat(auto-fill, minmax(160px, 1fr));
  grid-gap: 20px;
  padding: 0 20px 60px 20px;
}
</style>
