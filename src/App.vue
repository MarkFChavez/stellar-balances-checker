<template>
  <div>
    <header class="p-4 mb-8 border-b-2 border-black text-center">
      <h1 class="font-normal">Bloom Microservices Checker</h1>
      <p> Check out how much BTC and PHP tokens we have in Stellar. </p>
    </header>

    <div>
      <BalanceChecker 
        title="Bloom Trade (Staging)" 
        :address="address" />
    </div>
  </div>
</template>

<script>
import BalanceChecker from "@/components/BalanceChecker"

export default {
  components: { BalanceChecker },
  data () {
    return {
      address: process.env.VUE_APP_STELLAR_ADDRESS,
      balances: []
    }
  },
}
</script>
