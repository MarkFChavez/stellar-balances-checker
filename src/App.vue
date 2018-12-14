<template>
  <div>
    <header class="p-4 mb-8 border-b-2 border-black text-center">
      <h1 class="font-normal">{{appTitle}}</h1>
      <p class="mb-3"> Check out how much Stellar tokens your services have! </p>
      <!-- Place this tag where you want the button to render. -->
      <a class="github-button" href="https://github.com/mrkjlchvz/stellar-balances-checker" data-icon="octicon-star" data-size="large" data-show-count="true" aria-label="Star mrkjlchvz/stellar-balances-checker on GitHub">Star</a>
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
