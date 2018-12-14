<template>
  <div>
    <header class="p-4 mb-8 border-b-2 border-black text-center">
      <h1 class="font-normal">{{appTitle}}</h1>
      <p> Check out how much Stellar tokens your services have! </p>
    </header>

    <div>
      <BalanceChecker
        v-for="(d, i) in data"
        :key="i"
        :title="d.title" 
        :address="d.address" />
    </div>
  </div>
</template>

<script>
import BalanceChecker from "@/components/BalanceChecker"
import data from "./fixtures.js"

export default {
  components: { BalanceChecker },
  data () {
    return {
      appTitle: process.env.VUE_APP_TITLE,
      data: data,
    }
  },
}
</script>
