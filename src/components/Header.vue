<template>
  <nav>
    <ul>
      <li>
        BriteCore
      </li>
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
    background-color: $header-background-color;
    color: white;
    height: 30px;
  }

  nav ul {
    align-items: center;
    display: flex;
    height: 100%;
    justify-content: space-between;
  }
</style>
