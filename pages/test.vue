<template>
  <div class="container">
    <div>
      <h1 class="title my-5">Nuxt.js + Typescript + Vuelidate demo</h1>
      <TestComponent />
    </div>
  </div>
</template>

<script lang="ts">
import { Component, Vue } from 'vue-property-decorator'
import TestComponent from '../components/TestComponent.vue'

@Component({
  components: {
    TestComponent,
  },
})
export default class TestPage extends Vue {}
</script>

<style></style>
