<template>
  <div id="app">
    <router-view/>
  </div>
</template>

<script>
export default {
  name: 'app'
}
</script>

<style lang="less">
@import url('assets/styles/base-styles.less');

html {
  font-family: @raleway;
  font-size: 16px;
  word-spacing: 1px;
  -ms-text-size-adjust: 100%;
  -webkit-text-size-adjust: 100%;
  -moz-osx-font-smoothing: grayscale;
  -webkit-font-smoothing: antialiased;
  background: rgb(255,66,207);
  background: -moz-linear-gradient(-45deg, rgba(255,66,207,1) 1%, rgba(125,185,232,1) 100%);
  background: -webkit-linear-gradient(-45deg, rgba(255,66,207,1) 1%,rgba(125,185,232,1) 100%);
  background: linear-gradient(135deg, rgba(255,66,207,1) 1%,rgba(125,185,232,1) 100%);
  filter: progid:DXImageTransform.Microsoft.gradient( startColorstr='#ff42cf', endColorstr='#7db9e8',GradientType=1 );
  min-height: 100vh;
}

*, *:before, *:after {
  box-sizing: border-box;
  margin: 0;
}
</style>
