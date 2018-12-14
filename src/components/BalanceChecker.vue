<template>
  <div class="border-l-4 border-blue mb-2 px-4 py-1">
    <div class="flex justify-between mb-6">
      <span class="text-lg uppercase"> {{title}} </span>
      <span class="text-lg"> {{shortAddress}} </span>
    </div>

    <div v-if="loading">
      Loading...
    </div>

    <ul v-else class="list-reset">
      <li v-for="(b, i) in assetBalances" :key="i">
        <div class="flex">
          <div class="w-24">
            <span> {{b.asset_code}} </span>
          </div>

          <span> {{b.balance}} </span>
        </div>
      </li>
    </ul>
  </div>
</template>

<script>
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
    shortAddress () {
      let head = this.address.slice(0, 4)
      let tail = this.address.slice(-4)

      return `${head}...${tail}`
    }
  }
}
</script>
