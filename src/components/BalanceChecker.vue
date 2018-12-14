<template>
  <div class="border-l-4 border-blue mb-6 p-4 bg-blue-lightest shadow">
    <div class="flex justify-between mb-6 pb-3 border-b border-black">
      <span class="text-lg uppercase"> {{title}} </span>
      <span class="text-lg font-semibold"> {{address | shortify}} </span>
    </div>

    <div v-if="loading">
      Loading...
    </div>

    <ul v-else class="list-reset">
      <li class="mb-4" v-for="(b, i) in assetBalances" :key="i">
        <div class="flex">
          <div class="w-24">
            <span class="rounded bg-black text-white px-2 py-1"> {{b.asset_code}} </span> 
          </div>

          <div> 
            <span class="tracking-wide"> {{b.balance | formatMoney}} </span> 
          </div>
        </div>
      </li>
    </ul>
  </div>
</template>

<script>
import numeral from "numeral"

const BASE_URL = "https://horizon-testnet.stellar.org"

export default {
  data () {
    return {
      loading: false,
      balances: [],
    }
  },
  props: {
    address: {
      type: String,
      required: true,
    },
    title: {
      type: String,
      required: true,
    }
  },
  mounted () {
    this.getBalancesFor(this.address)
  },
  methods: {
    getBalancesFor(address) {
      this.loading = true

      fetch(BASE_URL + "/accounts/" + address).
        then(response => response.json()).
        then(data => this.balances = data.balances).
        finally(() => this.loading = false)
    }
  },
  computed: {
    assetBalances () {
      return this.balances.filter(function(balance) {
        return balance.asset_type !== "native"
      })
    },
  },
  filters: {
    formatMoney (number) {
      return numeral(number).format("0,0.00")
    },
    shortify (address) {
      let head = address.slice(0, 4)
      let tail = address.slice(-4)

      return `${head}...${tail}`
    }
  }
}
</script>
