<template>
  <div class="page2">
    <h1>{{ msg }}</h1>
    <h2>Testing out Vue Router with Express</h2>
    <p><a href="/" title="Back">Back</a></p>
  </div>
</template>

<script>
export default {
  name: 'Page2',
  data () {
    return {
      msg: 'This is another page'
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h1, h2 {
  font-weight: normal;
}

p {
  margin: .5em auto 0;
}

a {
  color: #42b983;
}
</style>
