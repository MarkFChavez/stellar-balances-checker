<template>
  <div>
    <header class="p-4 mb-8 border-b-2 border-black text-center">
      <h1 class="font-normal">{{appTitle}}</h1>
      <p> Check out how much BTC and PHP tokens we have in Stellar. </p>
    </header>

    <div>
      <BalanceChecker 
        :title="btTitle" 
        :address="btAddress" />

      <BalanceChecker 
        :title="palawanTitle" 
        :address="palawanAddress" />
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
      btTitle: process.env.VUE_APP_BT,
      btAddress: process.env.VUE_APP_BT_STELLAR_ADDRESS,
      palawanTitle: process.env.VUE_APP_TELLER_PALAWAN,
      palawanAddress: process.env.VUE_APP_TELLER_PALAWAN_STELLAR_ADDRESS,
    }
  },
}
</script>
