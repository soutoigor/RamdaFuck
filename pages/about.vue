<template>
  <Fragment>
    <Header />
    <main>
      <about-content />
    </main>
    <aside>
      <accessibility-area />
    </aside>
  </Fragment>
</template>

<script>
import { Fragment } from 'vue-fragment'
import Header from '~/layouts/Header'
import AccessibilityArea from '~/layouts/AccessibilityArea'
import AboutContent from '~/layouts/AboutContent'

export default {
  components: {
    Header,
    Fragment,
    AccessibilityArea,
    AboutContent,
  },
}
</script>

<style lang="stylus" scoped>
.hello
  color red
</style>
