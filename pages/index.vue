<template>
  <div class="container">
    <div>
      <p class="text-center"><Logo /></p>
      <h1 class="title">Demo Vue.js + typescript + PolkadotJS</h1>
      <pre class="mt-2">{{ JSON.stringify(stakingInfo, null, 2) }}</pre>
    </div>
  </div>
</template>

<script lang="ts">
import Vue from 'vue'
import { ApiPromise, WsProvider } from '@polkadot/api'
const nodeWs = 'wss://kusama-rpc.polkadot.io'
const authorityId = 'GTzRQPzkcuynHgkEHhsPBFpKdh4sAacVRsnd8vYfPpTMeEY'

export default Vue.extend({
  data() {
    return {
      stakingInfo: {},
    }
  },
  async created() {
    const wsProvider = new WsProvider(nodeWs)
    const api = await ApiPromise.create({ provider: wsProvider })
    this.stakingInfo = await api.derive.staking.query(authorityId, {
      withDestination: true,
      withExposure: true,
      withLedger: true,
      withNominations: true,
      withPrefs: true,
    })
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
