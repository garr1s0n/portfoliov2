<template>
  <section>
    <div id="header-section" class="content">
        <header-sec />
    </div>
    <div id="contact-section" class="content">
        <contact />
    </div>
  </section>
</template>

<script>
import HeaderSec from '../components/Header-Section.vue'
import Contact from '../components/Contact.vue'

export default {
    data () {
        return {
        }
    },
    components: {
        HeaderSec,
        Contact
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
