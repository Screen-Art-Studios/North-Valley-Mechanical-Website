<template>
  <div class="main">
    <h2>480-538-9184</h2>
    <h1>&#169;Copyright 2018 North Valley Mechanical</h1>
  </div>
</template>

<script>
  export default {
    name: 'Footer',
    data () {
      return {}
    }
  }
</script>

<style scoped lang='less'>
  .main {
    position: fixed;
    left: 0;
    bottom: 0;
    width: 100%;
    height: 7%;
    color: white;
    text-align: center;
    background: linear-gradient(#005DA6, #014271);
  }

  h1 {
    bottom: 0;
    z-index: 13;
    position: fixed;
    font-weight: lighter;
    font-size: .8em;
    color: #fff;
    text-align: center;
    line-height: 1;
    width: 100%;
    margin-right: 12px;
    letter-spacing: 1px;
    margin-bottom: 5px;
  }

  h2 {
    bottom: 0;
    z-index: 13;
    position: fixed;
    font-weight: lighter;
    font-size: 1em;
    color: #fff;
    text-align: center;
    line-height: 1;
    width: 100%;
    letter-spacing: 1px;
    margin-bottom: 20px;
  }

  @media (min-width: 700px) {
  }
</style>
