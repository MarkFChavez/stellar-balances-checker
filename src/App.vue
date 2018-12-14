<template>
  <div>
    <header class="p-4 mb-8 border-b-2 border-black text-center">
      <h1 class="font-normal">{{appTitle}}</h1>
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
      appTitle: process.env.VUE_APP_TITLE,
      address: process.env.VUE_APP_STELLAR_ADDRESS,
    }
  },
}
</script>
