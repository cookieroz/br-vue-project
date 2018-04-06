<template>
  <div>
    <h1>roz main App</h1>
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

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
