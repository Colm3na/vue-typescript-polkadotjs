<template>
  <div>
    <b-form-input
      v-model="accountId"
      placeholder="Enter your Kusama address"
      aria-describedby="address-feedback"
      :state="validateState('accountId')"
      @input="validate()"
    ></b-form-input>
    <b-form-invalid-feedback id="address-feedback"
      >Not a valid kusama address
    </b-form-invalid-feedback>
  </div>
</template>

<script lang="ts">
import Vue from 'vue'
import Vuelidate from 'vuelidate'
import { Component } from 'vue-property-decorator'
import { required } from 'vuelidate/lib/validators'
import { checkAddress } from "@polkadot/util-crypto";
Component.registerHooks(['validations'])
Vue.use(Vuelidate)

const addressPrefix: number = 2

const isValidPolkadotAddress = (address: string) => {
  return checkAddress(address, addressPrefix)[0]
}

@Component
export default class App extends Vue {
  // Data properties
  accountId: string = ''
  $v: any

  // Lifecycle hook
  mounted() {
    // blah blah blah
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

  public validate(): void {
    this.$v.$touch()
    console.log(this.$v)
  }
}
</script>
