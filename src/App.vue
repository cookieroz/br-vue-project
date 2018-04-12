<template>
  <div class="br-code-test-app">
    <app-header></app-header>
    <add-field></add-field>
  </div>
</template>

<script>
import Header from './components/Header.vue';
import AddField from './components/AddField.vue';

export default {
  name: 'App',
  components: {
    'app-header': Header,
    'add-field': AddField
  }
}
</script>

<style lang="scss">
  @import 'assets/scss/global';
</style>
