<template>
  <section>
    <div id="header-section" class="content">
        <header-sec />
    </div>
    <div id="contact-section" class="content">
    </div>
  </section>
</template>

<script>
import HeaderSec from '../components/Header-Section.vue'

export default {
    data () {
        return {
            message: 'Hello World'
        }
    },
    components: {
        HeaderSec
    }
}
</script>

<style lang="less">
@import url('../assets/styles/base-styles.less');

.content {
  min-height: 100vh;
  padding: 2em 0;
  display: flex;
  justify-content: center;
  align-items: center;
}
</style>
