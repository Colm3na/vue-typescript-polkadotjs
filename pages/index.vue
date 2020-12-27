<template>
  <div class="container">
    <div>
      <p class="text-center"><Logo /></p>
      <h1 class="title">
        Nuxt.js + Vue.js + Typescript + Vuelidate + PolkadotJS
      </h1>
      <Balances />
    </div>
  </div>
</template>

<script lang="ts">
import { Component, Vue } from 'vue-property-decorator'
import Balances from '@/components/Balances.vue'

@Component({
  components: {
    Balances,
  },
})
export default class App extends Vue {}
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
