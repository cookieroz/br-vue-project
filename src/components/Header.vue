<template>
  <nav>
    <div class="logo">
      BriteCore
    </div>
    <ul>
      <li>policies</li>
      <li>claims</li>
      <li>contacts</li>
      <li>data</li>
      <li>lines</li>
      <li>all modules</li>
    </ul>
  </nav>
</template>

<script>
export default {}
</script>

<style lang="scss">
  @import '../assets/scss/_mixins';

  nav {
    align-items: center;
    background-color: $header-background-color;
    color: white;
    display: flex;
    height: 30px;
    padding: 0 15px;

    .logo {
      margin-right: 30px;
    }

    ul {
      height: 100%;
    }

    li {
      display: inline-block;
      line-height: 30px;
      padding: 0 5px;
    }
  }
</style>
