<template>
  <Fragment>
    <Header />
    <index-container />
  </Fragment>
</template>

<script>
import { Fragment } from 'vue-fragment'
import Header from '~/layouts/Header'
import IndexContainer from '~/layouts/IndexContainer.vue'

export default {
  components: {
    Header,
    IndexContainer,
    Fragment,
  },
}
</script>
