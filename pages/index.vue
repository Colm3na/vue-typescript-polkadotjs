<template>
  <div class="container">
    <div>
      <p class="text-center"><Logo /></p>
      <h1 class="title">Nuxt.js + Vue.js + Typescript + PolkadotJS demo</h1>
      <b-input-group class="my-3">
        <b-form-input
          v-model="accountId"
          placeholder="Enter your Kusama address"
        ></b-form-input>
        <b-input-group-append>
          <b-button variant="success" @click="getBalances()"
            >Get Balance</b-button
          >
        </b-input-group-append>
      </b-input-group>
      <pre class="mt-2">{{ JSON.stringify(balances, null, 2) }}</pre>
    </div>
  </div>
</template>

<script lang="ts">
import Vue from 'vue'
import { ApiPromise, WsProvider } from '@polkadot/api'
const nodeWs = 'wss://kusama-rpc.polkadot.io'

export default Vue.extend({
  data() {
    return {
      api: {} as any,
      accountId: '' as string,
      balances: {} as any,
    }
  },
  async created() {
    const wsProvider = new WsProvider(nodeWs)
    this.api = await ApiPromise.create({ provider: wsProvider })
  },
  methods: {
    async getBalances(): Promise<void> {
      this.balances = await this.api.derive.balances.all(this.accountId)
    },
  },
})
</script>

<style>
.container {
  margin: 0 auto;
  min-height: 100vh;
  display: flex;
}

.title {
  font-family: 'Quicksand', 'Source Sans Pro', -apple-system, BlinkMacSystemFont,
    'Segoe UI', Roboto, 'Helvetica Neue', Arial, sans-serif;
  display: block;
  font-weight: 300;
  font-size: 70px;
  color: #35495e;
  letter-spacing: 1px;
  text-align: center;
}

.subtitle {
  font-weight: 300;
  font-size: 42px;
  color: #526488;
  word-spacing: 5px;
  padding-bottom: 15px;
}

pre {
  background-color: rgb(43, 44, 44);
  color: rgb(78, 238, 104);
  padding: 2rem 4rem;
}
</style>
