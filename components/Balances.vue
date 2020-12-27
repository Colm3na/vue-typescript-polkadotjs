<template>
  <div>
    <b-row>
      <b-col cols="10">
        <b-form-input
          v-model="accountId"
          placeholder="Enter your Kusama address"
          aria-describedby="address-feedback"
          :state="validateState('accountId')"
        ></b-form-input>
      </b-col>
      <b-col cols="2">
        <b-button
          variant="success"
          class="btn-block"
          @click="getBalances()"
          :disabled="this.$v.$invalid"
          >Get Balance</b-button
        >
      </b-col>
    </b-row>
    <b-form-invalid-feedback id="address-feedback"
      >Not a valid kusama address
    </b-form-invalid-feedback>
    <pre class="mt-4">{{ JSON.stringify(balances, null, 2) }}</pre>
  </div>
</template>

<script lang="ts">
import Vue from 'vue'
import Vuelidate from 'vuelidate'
import { Component } from 'vue-property-decorator'
import { required } from 'vuelidate/lib/validators'
import { checkAddress } from '@polkadot/util-crypto'
import { ApiPromise, WsProvider } from '@polkadot/api'
Component.registerHooks(['validations'])
Vue.use(Vuelidate)

const nodeWs = 'wss://kusama-rpc.polkadot.io'
const addressPrefix: number = 2

const isValidPolkadotAddress = (address: string) => {
  return checkAddress(address, addressPrefix)[0]
}

@Component
export default class App extends Vue {
  // Data properties
  accountId: string = ''
  $v: any = {}
  api: any = {}
  balances: any = {}

  async created() {
    this.$v.$touch()
    const wsProvider = new WsProvider(nodeWs)
    this.api = await ApiPromise.create({ provider: wsProvider })
  }

  // Vuelidate validations
  validations() {
    return {
      accountId: { required, isValidPolkadotAddress },
    }
  }

  // Component methods
  public validateState(name: string): any {
    const { $dirty, $error } = this.$v[name]
    return $dirty ? !$error : null
  }

  public async getBalances(): Promise<void> {
    this.balances = await this.api.derive.balances.all(this.accountId)
  }
}
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